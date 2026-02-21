# SnapStats Complete Product Specification
## snapstats.app

This is the single source of truth for building SnapStats. Everything Claude Code needs is in this document: the product vision, portal architecture, feature specs, pricing system, design system, and the landing page. Read the whole thing before writing any code.

---

## TABLE OF CONTENTS

1. Product Vision and Core Narrative
2. How SnapStats Works (The Full Loop)
3. User Roles and Portals Overview
4. Portal 1: Admin Portal (Desktop)
5. Portal 2: Coach Portal (Desktop)
6. Portal 3: Player Portal (Mobile)
7. Portal 4: Parent Portal (Mobile)
8. Multi-Tracker Consensus System
9. Player Homework / Film Study Mode
10. Database Schema Additions
11. Pricing Architecture and Subscription System
12. Design System
13. Landing Page (/about)
14. Technical Requirements

---

## 1. Product Vision and Core Narrative

### The Problem

If you're tracking stats live during a game, you're missing the game. You can't watch your kid score a goal and log it on a clipboard at the same time. You miss context. You miss plays. You guess. And when you have one person frantically tracking stats courtside, the data quality suffers. Garbage in, garbage out.

### The Solution

SnapStats flips the model. Record the game with any camera. Watch it live. Enjoy it. Then go home, upload the video to SnapStats, and track every stat frame by frame on your desktop. Pause. Rewind. See exactly what happened. No more missed stats. No more guessing.

When the stats are done, the magic begins. Click any stat and the video jumps to two seconds before that play. Instantly. Every goal, every assist, every steal, every turnover is linked to the exact moment it happened in the footage.

Then the real fun starts. Players log in on their phones and see their own stats, their progression, and video of every play they were involved in. Parents log in and see their child's profile: stats, highlights, and the ability to tap any stat and watch that moment. They never see the work of stat tracking. They just see the magic.

### The Differentiators

1. **Watch the game, track it later.** No more choosing between being present and doing your job.
2. **Frame-by-frame precision.** Pause, rewind, track with accuracy you'd never get live.
3. **Click any stat, see the play.** Every stat timestamped to video. Instant playback.
4. **Multi-tracker consensus.** Multiple people stat the same game. The system produces the most accurate stat layer possible. Solves the GIGO problem.
5. **Player film study homework.** Players stat games as homework. Compare their version against the coach's. Teaches game IQ through film.
6. **Every sport, one platform.** 15+ sports. Data-driven configs. Adding a new sport is database config, not code.
7. **Four portals, one engine.** Admin, Coach, Player, Parent. Each sees exactly what they need.
8. **Affordable for youth clubs.** Not enterprise pricing.

### The Viral Loop

Coach tracks the game. Parent opens their phone. Sees their kid scored 3 goals. Taps one. Watches the play. Shows every other parent. Those parents ask their coach "why don't we have this?" That's how SnapStats grows.

---

## 2. How SnapStats Works (The Full Loop)

### Step 1: Record the Game
Someone at the game records it. Phone, tablet, GoPro, camcorder, whatever. Just hit record. Watch the game. Be present.

### Step 2: Upload the Video
After the game (could be that night, could be the next day, could be a week later), the coach or a designated person uploads the video to SnapStats on their desktop.

### Step 3: Track Stats Frame by Frame
On the desktop, the coach opens the video in the SnapStats tracking interface. Video player on one side, stat panel on the other. They watch the game at their own pace. Pause to tag a play. Rewind to catch something they missed. Log every event: goals, assists, shots, steals, blocks, fouls, turnovers, whatever the sport calls for. Each stat entry is automatically timestamped to the video frame.

### Step 4: The Stats Layer is Complete
The game now has a complete stat layer linked to the video. Every event is a clickable timestamp.

### Step 5: Multi-Tracker Refinement (Optional but Powerful)
The coach assigns the game as homework. Each player (or parent volunteer, or assistant coach) stats the same game independently. SnapStats collects all versions, compares them, identifies consensus and discrepancies, and produces a refined "best" stat layer. More trackers = more accurate data.

### Step 6: Players See Their Profile
Players log into SnapStats on their phone. They see their stats for the game. Tap any stat and watch the video clip of that play. See their season averages, progression charts, and personal highlights. They never see the tracking interface. They just see the results.

### Step 7: Parents See Their Child
Parents log in on their phone. They see their child's profile. Stats, highlights, video clips of every play their kid was involved in. They can share clips. They can track progression over the season. They never see the stat tracking work. They just see their child performing.

### Step 8: Coach Reviews and Analyzes
The coach uses the desktop portal to review team analytics, compare player performance, build game plans, and prepare for the next opponent. Export reports as CSV or PDF. Review film with the team.

---

## 3. User Roles and Portals Overview

### Four Portals, One Engine

| Portal | Primary User | Device | Purpose |
|--------|-------------|--------|---------|
| Admin | Athletic Director, Club President | Desktop | Program oversight, billing, team/user management |
| Coach | Head Coach, Assistant Coach, Stat Tracker | Desktop | Upload video, track stats, analyze, game plan |
| Player | Athletes | Mobile | View own stats, watch own highlights, track progression |
| Parent | Parents, Family | Mobile | View child's stats, watch child's highlights, share moments |

### Role Hierarchy and Permissions

```typescript
export type UserRole = 'admin' | 'coach' | 'assistant_coach' | 'stat_tracker' | 'player' | 'parent';

export interface RolePermissions {
  // Program level
  canManageProgram: boolean;
  canViewAllTeams: boolean;
  canManageBilling: boolean;

  // Team level
  canManageRoster: boolean;
  canInviteUsers: boolean;
  canUploadVideo: boolean;
  canTrackStats: boolean;
  canEditStats: boolean;
  canDeleteGames: boolean;
  canAssignHomework: boolean;
  canViewHomeworkResults: boolean;

  // Viewing
  canViewAllPlayerStats: boolean;
  canViewOwnStats: boolean;
  canViewChildStats: boolean;
  canViewFullGameFilm: boolean;
  canViewPlayerHighlights: boolean;
  canExportData: boolean;

  // Analytics
  canViewTeamAnalytics: boolean;
  canViewPlayerAnalytics: boolean;
  canViewSeasonTrends: boolean;
  canViewMultiTrackerConsensus: boolean;
}

export const ROLE_PERMISSIONS: Record<UserRole, RolePermissions> = {
  admin: {
    canManageProgram: true,
    canViewAllTeams: true,
    canManageBilling: true,
    canManageRoster: true,
    canInviteUsers: true,
    canUploadVideo: true,
    canTrackStats: true,
    canEditStats: true,
    canDeleteGames: true,
    canAssignHomework: true,
    canViewHomeworkResults: true,
    canViewAllPlayerStats: true,
    canViewOwnStats: true,
    canViewChildStats: false,
    canViewFullGameFilm: true,
    canViewPlayerHighlights: true,
    canExportData: true,
    canViewTeamAnalytics: true,
    canViewPlayerAnalytics: true,
    canViewSeasonTrends: true,
    canViewMultiTrackerConsensus: true,
  },
  coach: {
    canManageProgram: false,
    canViewAllTeams: false,
    canManageBilling: false,
    canManageRoster: true,
    canInviteUsers: true,
    canUploadVideo: true,
    canTrackStats: true,
    canEditStats: true,
    canDeleteGames: true,
    canAssignHomework: true,
    canViewHomeworkResults: true,
    canViewAllPlayerStats: true,
    canViewOwnStats: false,
    canViewChildStats: false,
    canViewFullGameFilm: true,
    canViewPlayerHighlights: true,
    canExportData: true,
    canViewTeamAnalytics: true,
    canViewPlayerAnalytics: true,
    canViewSeasonTrends: true,
    canViewMultiTrackerConsensus: true,
  },
  assistant_coach: {
    canManageProgram: false,
    canViewAllTeams: false,
    canManageBilling: false,
    canManageRoster: false,
    canInviteUsers: false,
    canUploadVideo: true,
    canTrackStats: true,
    canEditStats: true,
    canDeleteGames: false,
    canAssignHomework: false,
    canViewHomeworkResults: true,
    canViewAllPlayerStats: true,
    canViewOwnStats: false,
    canViewChildStats: false,
    canViewFullGameFilm: true,
    canViewPlayerHighlights: true,
    canExportData: true,
    canViewTeamAnalytics: true,
    canViewPlayerAnalytics: true,
    canViewSeasonTrends: true,
    canViewMultiTrackerConsensus: true,
  },
  stat_tracker: {
    canManageProgram: false,
    canViewAllTeams: false,
    canManageBilling: false,
    canManageRoster: false,
    canInviteUsers: false,
    canUploadVideo: false,
    canTrackStats: true,
    canEditStats: false,
    canDeleteGames: false,
    canAssignHomework: false,
    canViewHomeworkResults: false,
    canViewAllPlayerStats: true,
    canViewOwnStats: false,
    canViewChildStats: false,
    canViewFullGameFilm: true,
    canViewPlayerHighlights: true,
    canExportData: false,
    canViewTeamAnalytics: false,
    canViewPlayerAnalytics: false,
    canViewSeasonTrends: false,
    canViewMultiTrackerConsensus: false,
  },
  player: {
    canManageProgram: false,
    canViewAllTeams: false,
    canManageBilling: false,
    canManageRoster: false,
    canInviteUsers: false,
    canUploadVideo: false,
    canTrackStats: true,           // for homework mode only
    canEditStats: false,
    canDeleteGames: false,
    canAssignHomework: false,
    canViewHomeworkResults: false,  // they see their own accuracy score only
    canViewAllPlayerStats: false,
    canViewOwnStats: true,
    canViewChildStats: false,
    canViewFullGameFilm: false,
    canViewPlayerHighlights: true,
    canExportData: false,
    canViewTeamAnalytics: false,
    canViewPlayerAnalytics: true,  // own only
    canViewSeasonTrends: true,     // own only
    canViewMultiTrackerConsensus: false,
  },
  parent: {
    canManageProgram: false,
    canViewAllTeams: false,
    canManageBilling: false,
    canManageRoster: false,
    canInviteUsers: false,
    canUploadVideo: false,
    canTrackStats: false,
    canEditStats: false,
    canDeleteGames: false,
    canAssignHomework: false,
    canViewHomeworkResults: false,
    canViewAllPlayerStats: false,
    canViewOwnStats: false,
    canViewChildStats: true,
    canViewFullGameFilm: false,
    canViewPlayerHighlights: true,
    canExportData: false,
    canViewTeamAnalytics: false,
    canViewPlayerAnalytics: true,  // child only
    canViewSeasonTrends: true,     // child only
    canViewMultiTrackerConsensus: false,
  },
};
```

### Invitation Flow

1. Coach creates a team, imports roster (player names, numbers, positions)
2. Coach invites assistant coaches and stat trackers via email
3. Coach invites players via email (or generates invite code for the team)
4. Players accept invite, create account, are linked to their roster entry
5. Players can invite their own parents (or coach bulk-invites parents)
6. Parents accept invite, create account, are linked to their child's player profile
7. A parent can have multiple children across multiple teams/sports
8. A player can have multiple parents linked

---

## 4. Portal 1: Admin Portal (Desktop-First)

### Who
Athletic directors, club presidents, program coordinators. The person who pays the bill.

### What They See

**Dashboard**
- Program stats: total teams, total athletes, total games tracked, total video hours
- Activity feed: recent games logged, recent uploads, new users joined
- Subscription card: current plan, usage vs limits, next billing date
- Quick actions: Add Team, Invite Coach, Manage Billing

**Teams Management**
- All teams grouped by sport
- Each team card: sport icon, team name, head coach, roster count, games this season, last activity
- Create team: pick sport, name, assign coach
- Archive/deactivate teams (data preserved, just hidden)

**Users Management**
- All users across program, filterable by role, team, sport, active/inactive
- Invite flow: email, role selection, team assignment
- Edit roles, reassign teams, deactivate users
- See last login, activity level

**Billing**
- Current plan, usage meters (teams, games, stat trackers vs limits)
- Plan comparison (shared PricingTable component)
- Payment history
- Manage payment method (Stripe Customer Portal)
- Cancel/downgrade flow with clear messaging about what they lose

**Program Analytics**
- Games tracked per team per month (bar chart)
- Most active teams/coaches
- Sport breakdown across program
- Growth over time (new athletes, new games)

### Design Notes
- Full sidebar nav, dark mode
- Data-dense dashboard style
- Subtle "Admin" badge in sidebar to differentiate from coach view
- Uses the standard SnapStats design system

---

## 5. Portal 2: Coach Portal (Desktop-First)

### Who
Head coaches, assistant coaches, stat trackers. The people who do the work.

### What They See

**Dashboard**
- Their teams (coach may have multiple)
- Recent games with status: Uploaded (video uploaded, not yet statted), In Progress (partially statted), Complete (fully statted), Homework Assigned
- Quick actions: Upload Video, Continue Tracking, Assign Homework
- Upcoming games (if schedule is entered)

**Game Upload**
- Upload video file (drag and drop or file picker)
- Select team and opponent
- Enter game date, location, score (optional)
- Video begins processing/uploading
- Once uploaded, transitions to tracking interface

**Stat Tracking Interface (THE CORE SCREEN)**

This is the most important screen in the entire product. Desktop-optimized.

Layout:
```
┌──────────────────────────────────────────────────────────┐
│  TOOLBAR: Game info | Save | Undo | Redo | Settings     │
├────────────────────────────┬─────────────────────────────┤
│                            │                             │
│     VIDEO PLAYER           │     STAT PANEL              │
│                            │                             │
│  ┌──────────────────────┐  │  Player selector (roster)   │
│  │                      │  │                             │
│  │    Game footage       │  │  Stat buttons by category: │
│  │                      │  │  ┌──────┐ ┌──────┐         │
│  │                      │  │  │ GOAL │ │ASSIST│         │
│  │                      │  │  └──────┘ └──────┘         │
│  └──────────────────────┘  │  ┌──────┐ ┌──────┐         │
│                            │  │ SHOT │ │STEAL │         │
│  Play / Pause / << / >>    │  └──────┘ └──────┘         │
│  Frame back / Frame fwd    │  ┌──────┐ ┌──────┐         │
│  Playback speed: 0.5x 1x  │  │BLOCK │ │ FOUL │         │
│                            │  └──────┘ └──────┘         │
│                            │                             │
│                            │  Recent entries (scrollable)│
│                            │  with undo on each          │
├────────────────────────────┴─────────────────────────────┤
│  TIMELINE BAR with stat markers plotted across it        │
│  ●  ●    ●  ●●   ●     ●  ●  ●    ●●●  ●   ●  ●      │
└──────────────────────────────────────────────────────────┘
```

**Video player controls:**
- Play / Pause (spacebar)
- Frame forward / Frame back (arrow keys)
- Skip forward 5s / Skip back 5s (shift+arrow)
- Playback speed: 0.25x, 0.5x, 1x, 1.5x, 2x
- Full-screen toggle
- Volume control

**Stat panel:**
- Player selector: dropdown or quick-select grid of jersey numbers
- Stat buttons: organized by category based on sport config
- Water polo example categories:
  - Offense: Goal, Assist, Shot on Goal, Shot Missed, Earned Exclusion, Turnover
  - Defense: Steal, Block, Caused Turnover
  - Goalie: Save, Goal Allowed
  - General: Exclusion (kicked out), Penalty Shot, Sprint Won, Sprint Lost
- Each button tap: logs the stat, timestamps it to current video frame, shows in recent entries
- Recent entries list: each entry shows player, stat type, timestamp, with individual undo button
- Undo (Ctrl+Z): removes last entry

**Keyboard shortcuts (critical for speed):**
- Number keys 1-9: select player by roster position or jersey number
- Letter keys mapped to common stats (G=Goal, A=Assist, S=Shot, etc.)
- Spacebar: play/pause
- Arrow keys: frame navigation
- Ctrl+Z: undo last stat entry
- All shortcuts shown in a help overlay (? key to toggle)

**Timeline bar:**
- Full-width bar showing the game timeline
- Colored markers for each stat entry (color-coded by stat type)
- Click any marker to jump video to that timestamp
- Drag to scrub through the game
- Shows quarter/period markers if entered

**Game Review Mode**
- After stats are complete, switch to review mode
- Stats displayed as a sortable, filterable list
- Click any stat row, video jumps to 2 seconds before that play
- Filter by player, stat type, period/quarter
- Box score summary view
- Shot chart (for applicable sports)
- Export: CSV, PDF game report

**Homework Assignment**
- From a completed game, coach clicks "Assign as Homework"
- Selects which players (or all) receive the assignment
- Sets optional due date
- Players get notification in their portal
- Coach can track who has completed it and view accuracy comparison

**Team Analytics**
- Per-player stat breakdowns
- Team totals per game
- Season averages and trends
- Comparison: this game vs season average
- Shot charts (for sports with location data)
- Player progression over time

**Roster Management**
- Add/edit/remove players
- Player info: name, number, position(s), photo (optional)
- Invite players to create accounts
- Link parents to players
- Import roster from CSV

### Design Notes
- Desktop-first, split-panel layout for tracking
- Dark mode default (reduces eye strain during long film sessions)
- Video player is the hero. Give it as much space as possible.
- Stat panel should be efficient but not cramped
- Keyboard shortcuts are essential. Power users will track entire games without touching the mouse.
- The tracking interface should feel like a professional video editing tool, not a web form

---

## 6. Portal 3: Player Portal (Mobile-First)

### Who
Athletes. Middle school through college age. They live on their phones.

### What They See

**My Profile (Home Screen)**
- Player photo, name, number, position, team
- Season stat summary: key stats for their sport in big numbers (JetBrains Mono)
- Water polo example: Goals: 12, Assists: 8, Steals: 15, Shots: 34, Shooting %: 35%
- Recent games list with their personal stat line per game

**Game Detail**
- Their stats for that specific game
- Each stat is a tappable row
- Tap any stat: video clip plays showing 3 seconds before to 3 seconds after the play
- The player sees ONLY clips of plays they were involved in, not full game film
- Share button on each clip (generates a short shareable link or saves clip to camera roll)

**My Progression**
- Season trend charts for key stats
- Game-by-game line charts
- Personal bests highlighted
- Comparison to team average (optional, coach can enable/disable)

**Homework (Film Study)**
- List of assigned games to stat
- Tap a game to open a mobile-optimized tracking interface
- Simpler than the coach's desktop version: just the video player and stat buttons, no timeline bar
- Player watches the game and tags stats for ALL players (not just themselves)
- When complete, they submit their version
- They see their accuracy score compared to the coach's version (after coach reviews)
- Accuracy breakdown: which stats they got right, which they missed, which they added incorrectly

**Notifications**
- New game stats available
- Homework assigned
- Homework results ready
- Season milestone achieved

### Design Notes
- Mobile-first, bottom tab navigation
- Profile / Games / Progression / Homework / Settings
- Clean, card-based layout
- Big stat numbers in JetBrains Mono
- Video clips play inline, not full-screen by default (tap to expand)
- Lime accents on personal bests and highlights
- Feel: like checking your stats in a sports app (ESPN, Strava vibes)
- Young audience: make it feel cool, not clinical
- CRITICAL: Players never see the tracking interface complexity. They see clean results only. The only exception is Homework mode, which has a simplified tracking UI.

---

## 7. Portal 4: Parent Portal (Mobile-First)

### Who
Parents, grandparents, family members. They want to see their kid play and feel connected.

### What They See

**My Child's Profile (Home Screen)**
- Child's photo, name, number, position, team, sport
- If parent has multiple children on SnapStats, a switcher at the top
- Season highlights: key stats in big friendly numbers
- Water polo example: "12 Goals this season" with a flame emoji or trending arrow if it's a personal best
- Latest game card: opponent, date, child's stat line, "Watch Highlights" button

**Game Detail**
- Child's stats for that game, presented as a clean card layout
- Each stat is tappable
- Tap: plays a video clip of that moment (3 sec before to 3 sec after)
- The parent ONLY sees clips where their child is involved
- No full game film access. Just the highlights.
- Share button: generates a link or saves clip to camera roll
- "Share to family" quick action

**Season View**
- All games this season in a list
- Child's stat line per game
- Simple trend: "Averaging 2.4 goals per game, up from 1.8 last month"
- Season progression chart (simple, not data-heavy)

**Highlights Reel (Future Feature, Teased)**
- Auto-compiled video of child's best moments from the season
- Generated from the highest-impact stat clips
- Shareable as a single video

**Notifications**
- "New game stats are ready! See how [Child Name] did against [Opponent]"
- Season milestones: "Emily just hit 50 career goals!"
- Homework completion (if parent wants visibility)

### Design Notes
- Mobile-first, absolute minimum complexity
- Bottom tab nav: Home / Games / Season / Settings
- WARM tone. This portal is emotional, not analytical.
- Use the child's name everywhere. "Emily scored 3 goals" not "Player #7 logged 3 goals"
- Big, tappable video thumbnails
- Stats should feel celebratory, not clinical
- No jargon. "Goals" not "Conversion rate." "Steals" not "Forced turnovers."
- No admin, no settings complexity. Just the good stuff.
- Sharing is first-class. Every clip, every stat card should be shareable.
- CRITICAL: Parents never see the stat tracking interface. They never see homework assignments. They never see the work. They only see the polished results and video moments.
- The parent portal is the viral engine. Make it so good that parents show other parents.

---

## 8. Multi-Tracker Consensus System

### The Problem with Single-Tracker Stats

One person tracking stats for a fast game will miss things. They'll misattribute plays. They'll tag the wrong player. In water polo, the action is constant and players are half-submerged. In basketball, fast breaks happen in seconds. A single tracker can only be so accurate.

This is the GIGO problem: garbage in, garbage out. Your analytics are only as good as your stat layer. Every other platform ignores this.

### The Solution: Crowd-Sourced Accuracy

SnapStats allows multiple people to independently stat the same game against the same video. The system then compares all versions and produces a consensus stat layer that is more accurate than any single tracker could produce.

### How It Works

1. A game video is uploaded to SnapStats
2. The coach stats the game (this is the "reference" version)
3. The coach assigns the game for additional tracking (homework, volunteer parents, assistant coaches)
4. Each assigned tracker independently watches the video and logs their stats
5. They cannot see anyone else's version until they submit their own
6. Once multiple versions are submitted, SnapStats runs the consensus algorithm

### Consensus Algorithm

```typescript
// lib/consensus.ts

export interface StatEntry {
  id: string;
  trackerId: string;
  playerId: string;
  statType: string;       // 'goal', 'assist', 'steal', etc.
  timestamp: number;       // video timestamp in seconds (float)
  gameId: string;
}

export interface ConsensusEntry {
  playerId: string;
  statType: string;
  timestamp: number;       // averaged timestamp from matching entries
  confidence: number;      // 0-1, based on how many trackers agreed
  agreedTrackers: string[];
  disagreedTrackers: string[];
  isDisputed: boolean;     // flagged for coach review if confidence < threshold
}

// Matching logic:
// Two stat entries from different trackers are considered "the same play" if:
// 1. Same stat type (goal, assist, etc.)
// 2. Same player attributed
// 3. Timestamps within a configurable window (default: 5 seconds for most sports)
//
// A stat is included in the consensus if:
// - Majority of trackers (>50%) logged it
// - OR the coach's version includes it (coach is weighted higher)
//
// A stat is flagged as disputed if:
// - Fewer than 50% of trackers agree
// - Different trackers attributed it to different players
// - Coach version conflicts with majority
//
// Confidence score:
// - 1.0 = all trackers agree (same player, same stat, same timeframe)
// - 0.8 = most trackers agree, minor timestamp variance
// - 0.5 = split decision, needs review
// - Below 0.5 = flagged for coach resolution

export interface ConsensusConfig {
  timestampWindowSeconds: number;  // how close timestamps need to be to match (default 5)
  coachWeight: number;             // how much extra weight coach version gets (default 2x)
  minimumAgreementRatio: number;   // minimum % of trackers who must agree (default 0.5)
  disputeThreshold: number;        // confidence below this triggers review flag (default 0.5)
}

export const DEFAULT_CONSENSUS_CONFIG: ConsensusConfig = {
  timestampWindowSeconds: 5,
  coachWeight: 2,
  minimumAgreementRatio: 0.5,
  disputeThreshold: 0.5,
};
```

### Coach Review of Consensus

After the consensus runs, the coach sees a review screen:

- Green entries: all trackers agree. High confidence. Auto-accepted.
- Yellow entries: majority agree but some disagree. Coach can accept or modify.
- Red entries: disputed. Coach must resolve manually.
- Missing entries: stats the coach logged that no other tracker caught (or vice versa).

The coach makes final decisions on disputed entries, then publishes the finalized stat layer. This becomes the official game stats.

### Accuracy Scoring

Each tracker gets an accuracy score for the game:

```typescript
export interface TrackerAccuracy {
  trackerId: string;
  gameId: string;
  totalCorrect: number;       // entries that matched the final consensus
  totalIncorrect: number;     // entries that were rejected
  totalMissed: number;        // entries in consensus they didn't log
  accuracyPercent: number;    // correct / (correct + incorrect + missed)
  byStatType: Record<string, {
    correct: number;
    incorrect: number;
    missed: number;
  }>;
}
```

This accuracy score is visible to:
- The coach (for all trackers)
- Each player (their own score only, in homework mode)
- The admin (aggregate accuracy across the program)

### Water Polo Example

A JV water polo game: 14 players on the team. Coach uploads the game film. Assigns it as homework to all 14 players. Each player watches the full game at home and stats every play. The coach also stats it.

Now you have 15 independent stat layers on the same game.

- 13 out of 15 trackers agree Player #5 scored a goal at the 4:23 mark. High confidence. Auto-accepted.
- 8 out of 15 say it was assisted by Player #3, but 5 say Player #8 made the assist. 2 didn't log an assist at all. Disputed. Coach reviews the clip and confirms it was #3.
- Player #11 logged a steal at 6:45 that only 2 other trackers caught. Below threshold. Coach reviews and confirms yes, it was a steal. The 12 who missed it get dinged on accuracy.

The result: the most accurate stat layer possible, AND every player on the team has improved their game awareness by studying film.

---

## 9. Player Homework / Film Study Mode

### Why This Exists

This started as a coaching tool for water polo, but it works for every sport. When players watch game film and actively track stats:

1. **They see the game from outside.** A player in the water can only see their immediate surroundings. Watching from the camera angle, they see the full field/court/pool. They understand positioning, spacing, and team movement.
2. **They understand cause and effect.** Why did that play work? Why did that turnover happen? When you're forced to tag every event, you watch more carefully than you ever would passively.
3. **They develop game IQ.** Over a season of homework, players start recognizing patterns. They see opportunities they missed during the game. Their awareness improves.
4. **The coach gets data quality.** 15 trackers produce better stats than 1. The homework serves double duty: teaching tool AND data collection.

### How Homework Mode Works

**Coach assigns:**
1. From a game with uploaded video, coach clicks "Assign Homework"
2. Selects recipients: all players, specific players, or a custom group
3. Sets due date (optional)
4. Adds optional instructions: "Focus on counting possessions" or "Pay special attention to defensive positioning"
5. Players get notified

**Player completes:**
1. Player opens the assignment in their mobile portal
2. Sees the game video in a simplified tracking interface
3. Mobile-optimized: video on top, stat buttons below, scrollable
4. They watch the game and log every stat for every player (not just themselves)
5. Player selector: tap a jersey number, then tap the stat
6. They can pause, rewind, replay sections
7. When done, they tap "Submit"
8. They CANNOT see the coach's version or any other player's version until after submission

**Coach reviews:**
1. Coach sees a homework dashboard: who has submitted, who hasn't
2. After enough submissions (or after due date), coach can run the consensus
3. Coach reviews the consensus, resolves disputes, publishes final stats
4. Accuracy scores are calculated for each player

**Player sees results:**
1. After coach publishes, player gets notified
2. They see their accuracy score: "You got 87% of the stats right"
3. Breakdown by stat type: "Goals: 95% accurate. Assists: 72% accurate. Steals: 81% accurate."
4. Specific misses: "You missed a steal by #7 at 12:34. Watch the clip."
5. Each miss links to the video moment so they can see what they overlooked
6. Over the season, they can track their accuracy improvement

### Homework Tracking Interface (Mobile)

Simpler than the coach's desktop version:

```
┌──────────────────────────┐
│  Game: vs Opponents      │
│  Due: Feb 20             │
├──────────────────────────┤
│                          │
│  ┌────────────────────┐  │
│  │                    │  │
│  │   Video Player     │  │
│  │                    │  │
│  └────────────────────┘  │
│  ▶ ⏸ ◀◀ ▶▶  1x        │
│                          │
│  Player: [#3 ▼]         │
│                          │
│  ┌─────┐ ┌─────┐        │
│  │GOAL │ │ASST │        │
│  └─────┘ └─────┘        │
│  ┌─────┐ ┌─────┐        │
│  │SHOT │ │STEAL│        │
│  └─────┘ └─────┘        │
│  ┌─────┐ ┌─────┐        │
│  │BLOCK│ │FOUL │        │
│  └─────┘ └─────┘        │
│                          │
│  Recent: Goal #3 @4:23  │
│          Steal #7 @4:41  │
│  [UNDO]                  │
│                          │
│  [SUBMIT HOMEWORK]       │
└──────────────────────────┘
```

- No timeline bar (too complex for mobile)
- Larger buttons than desktop (touch targets)
- Player selector is prominent (they're tagging plays for the whole team)
- Recent entries with undo
- Progress indicator: estimated % of game statted based on video position
- Save progress and continue later

---

## 10. Database Schema Additions

### Multi-Tracker and Homework Tables

```sql
-- Stat tracking sessions: one per tracker per game
create table if not exists stat_sessions (
  id uuid primary key default gen_random_uuid(),
  game_id uuid references games(id) not null,
  tracker_id uuid references users(id) not null,
  tracker_role text not null,           -- 'coach', 'player', 'assistant_coach', 'stat_tracker'
  is_reference boolean default false,   -- true if this is the coach's "official" version
  is_homework boolean default false,    -- true if this was assigned as homework
  homework_id uuid references homework_assignments(id),
  status text default 'in_progress',    -- 'in_progress', 'submitted', 'reviewed'
  submitted_at timestamptz,
  accuracy_score decimal(5,2),          -- calculated after consensus
  created_at timestamptz default now(),
  updated_at timestamptz default now(),
  unique(game_id, tracker_id)
);

-- Individual stat entries within a session
create table if not exists stat_entries (
  id uuid primary key default gen_random_uuid(),
  session_id uuid references stat_sessions(id) not null,
  game_id uuid references games(id) not null,
  player_id uuid references players(id) not null,
  stat_type text not null,              -- sport-specific: 'goal', 'assist', 'steal', etc.
  video_timestamp decimal(10,3),        -- seconds from start of video, millisecond precision
  period integer,                       -- quarter, half, period number
  metadata jsonb default '{}',          -- sport-specific extra data (shot location, etc.)
  created_at timestamptz default now()
);

create index idx_stat_entries_session on stat_entries(session_id);
create index idx_stat_entries_game on stat_entries(game_id);
create index idx_stat_entries_player on stat_entries(player_id);
create index idx_stat_entries_timestamp on stat_entries(game_id, video_timestamp);

-- Consensus results
create table if not exists consensus_entries (
  id uuid primary key default gen_random_uuid(),
  game_id uuid references games(id) not null,
  player_id uuid references players(id) not null,
  stat_type text not null,
  video_timestamp decimal(10,3),
  confidence decimal(3,2),              -- 0.00 to 1.00
  status text default 'auto_accepted',  -- 'auto_accepted', 'disputed', 'coach_resolved', 'rejected'
  resolved_by uuid references users(id),
  agreed_tracker_ids uuid[] default '{}',
  disagreed_tracker_ids uuid[] default '{}',
  metadata jsonb default '{}',
  created_at timestamptz default now()
);

create index idx_consensus_game on consensus_entries(game_id);

-- Homework assignments
create table if not exists homework_assignments (
  id uuid primary key default gen_random_uuid(),
  game_id uuid references games(id) not null,
  assigned_by uuid references users(id) not null,
  team_id uuid references teams(id) not null,
  instructions text,
  due_date timestamptz,
  status text default 'assigned',       -- 'assigned', 'in_progress', 'completed', 'reviewed'
  created_at timestamptz default now()
);

-- Homework recipients (which players got the assignment)
create table if not exists homework_recipients (
  id uuid primary key default gen_random_uuid(),
  homework_id uuid references homework_assignments(id) not null,
  player_id uuid references players(id) not null,
  user_id uuid references users(id),    -- linked user account (if player has signed up)
  status text default 'assigned',        -- 'assigned', 'in_progress', 'submitted', 'reviewed'
  submitted_at timestamptz,
  accuracy_score decimal(5,2),
  accuracy_breakdown jsonb default '{}', -- per stat type accuracy
  created_at timestamptz default now(),
  unique(homework_id, player_id)
);

-- Parent-child links
create table if not exists parent_child_links (
  id uuid primary key default gen_random_uuid(),
  parent_user_id uuid references users(id) not null,
  player_id uuid references players(id) not null,
  relationship text default 'parent',    -- 'parent', 'guardian', 'family'
  created_at timestamptz default now(),
  unique(parent_user_id, player_id)
);
```

---

## 11. Pricing Architecture and Subscription System

### Plan Definitions

Single source of truth. The landing page, the app feature gates, and Stripe all read from this config.

```typescript
export type PlanId = 'starter' | 'pro' | 'program' | 'enterprise';
export type BillingInterval = 'monthly' | 'yearly';

export interface PlanFeatures {
  maxTeams: number;              // -1 for unlimited
  maxSports: number;             // -1 for unlimited
  maxGamesPerMonth: number;      // -1 for unlimited
  maxStatTrackers: number;       // -1 for unlimited
  filmSync: boolean;
  analyticsDashboards: boolean;
  csvExport: boolean;
  pdfExport: boolean;
  playerProfiles: boolean;
  parentPortal: boolean;
  seasonTrends: boolean;
  multiTracker: boolean;
  homeworkMode: boolean;
  consensusEngine: boolean;
  prioritySupport: boolean;
  sso: boolean;
  apiAccess: boolean;
  whiteLabel: boolean;
  dedicatedOnboarding: boolean;
}

export interface Plan {
  id: PlanId;
  name: string;
  tagline: string;
  monthlyPrice: number;       // cents. 0 = free. -1 = custom.
  yearlyPrice: number;        // cents. 0 = free. -1 = custom.
  features: PlanFeatures;
  highlighted: boolean;
  ctaLabel: string;
  ctaAction: 'signup' | 'contact';
  trialDays: number;
  stripePriceIdMonthly?: string;
  stripePriceIdYearly?: string;
}

export const PLANS: Plan[] = [
  {
    id: 'starter',
    name: 'Starter',
    tagline: 'Try SnapStats with zero commitment',
    monthlyPrice: 0,
    yearlyPrice: 0,
    features: {
      maxTeams: 1,
      maxSports: 1,
      maxGamesPerMonth: 3,
      maxStatTrackers: 1,
      filmSync: false,
      analyticsDashboards: false,
      csvExport: false,
      pdfExport: false,
      playerProfiles: false,
      parentPortal: false,
      seasonTrends: false,
      multiTracker: false,
      homeworkMode: false,
      consensusEngine: false,
      prioritySupport: false,
      sso: false,
      apiAccess: false,
      whiteLabel: false,
      dedicatedOnboarding: false,
    },
    highlighted: false,
    ctaLabel: 'START FREE TRIAL',
    ctaAction: 'signup',
    trialDays: 14,
  },
  {
    id: 'pro',
    name: 'Pro',
    tagline: 'Everything a team needs',
    monthlyPrice: 2900,
    yearlyPrice: 24900,
    features: {
      maxTeams: 1,
      maxSports: 1,
      maxGamesPerMonth: -1,
      maxStatTrackers: 3,
      filmSync: true,
      analyticsDashboards: true,
      csvExport: true,
      pdfExport: true,
      playerProfiles: true,
      parentPortal: true,
      seasonTrends: false,
      multiTracker: false,
      homeworkMode: false,
      consensusEngine: false,
      prioritySupport: false,
      sso: false,
      apiAccess: false,
      whiteLabel: false,
      dedicatedOnboarding: false,
    },
    highlighted: true,
    ctaLabel: 'START FREE TRIAL',
    ctaAction: 'signup',
    trialDays: 14,
  },
  {
    id: 'program',
    name: 'Program',
    tagline: 'For multi-team programs and athletic directors',
    monthlyPrice: 7900,
    yearlyPrice: 69900,
    features: {
      maxTeams: -1,
      maxSports: -1,
      maxGamesPerMonth: -1,
      maxStatTrackers: -1,
      filmSync: true,
      analyticsDashboards: true,
      csvExport: true,
      pdfExport: true,
      playerProfiles: true,
      parentPortal: true,
      seasonTrends: true,
      multiTracker: true,
      homeworkMode: true,
      consensusEngine: true,
      prioritySupport: true,
      sso: false,
      apiAccess: false,
      whiteLabel: false,
      dedicatedOnboarding: false,
    },
    highlighted: false,
    ctaLabel: 'START FREE TRIAL',
    ctaAction: 'signup',
    trialDays: 14,
  },
  {
    id: 'enterprise',
    name: 'Enterprise',
    tagline: 'For colleges and large athletic departments',
    monthlyPrice: -1,
    yearlyPrice: -1,
    features: {
      maxTeams: -1,
      maxSports: -1,
      maxGamesPerMonth: -1,
      maxStatTrackers: -1,
      filmSync: true,
      analyticsDashboards: true,
      csvExport: true,
      pdfExport: true,
      playerProfiles: true,
      parentPortal: true,
      seasonTrends: true,
      multiTracker: true,
      homeworkMode: true,
      consensusEngine: true,
      prioritySupport: true,
      sso: true,
      apiAccess: true,
      whiteLabel: true,
      dedicatedOnboarding: true,
    },
    highlighted: false,
    ctaLabel: 'CONTACT US',
    ctaAction: 'contact',
    trialDays: 0,
  },
];
```

### Feature Gating

```typescript
export function canAccess(userPlan: PlanId, feature: keyof PlanFeatures): boolean {
  const plan = PLANS.find(p => p.id === userPlan);
  if (!plan) return false;
  const value = plan.features[feature];
  if (typeof value === 'boolean') return value;
  if (typeof value === 'number') return value !== 0;
  return false;
}

export function getLimit(userPlan: PlanId, feature: keyof PlanFeatures): number {
  const plan = PLANS.find(p => p.id === userPlan);
  if (!plan) return 0;
  const value = plan.features[feature];
  if (typeof value === 'number') return value;
  return 0;
}

export function isAtLimit(userPlan: PlanId, feature: keyof PlanFeatures, currentCount: number): boolean {
  const limit = getLimit(userPlan, feature);
  if (limit === -1) return false;
  return currentCount >= limit;
}
```

### Subscription Schema

```sql
create table if not exists subscriptions (
  id uuid primary key default gen_random_uuid(),
  club_id uuid references clubs(id) not null,
  plan_id text not null default 'starter',
  status text not null default 'trialing',
  billing_interval text default 'monthly',
  trial_start timestamptz default now(),
  trial_end timestamptz default (now() + interval '14 days'),
  current_period_start timestamptz,
  current_period_end timestamptz,
  stripe_customer_id text,
  stripe_subscription_id text,
  stripe_price_id text,
  cancel_at_period_end boolean default false,
  canceled_at timestamptz,
  created_at timestamptz default now(),
  updated_at timestamptz default now(),
  unique(club_id)
);
```

### Subscription Helpers

```typescript
export function effectivePlan(sub: Subscription): PlanId {
  if (isTrialing(sub)) return 'pro';
  if (!isActive(sub)) return 'starter';
  return sub.planId;
}

export function isTrialing(sub: Subscription): boolean {
  return sub.status === 'trialing' && sub.trialEnd != null && new Date() < sub.trialEnd;
}

export function isActive(sub: Subscription): boolean {
  return sub.status === 'active' || isTrialing(sub);
}

export function daysLeftInTrial(sub: Subscription): number {
  if (!isTrialing(sub) || !sub.trialEnd) return 0;
  return Math.max(0, Math.ceil((sub.trialEnd.getTime() - Date.now()) / 86400000));
}
```

### Stripe Integration Stubs

Create these API route files with TODO comments:
- `app/api/stripe/create-checkout/route.ts`
- `app/api/stripe/create-portal/route.ts`
- `app/api/stripe/webhook/route.ts`

Webhook events to handle: `checkout.session.completed`, `customer.subscription.updated`, `customer.subscription.deleted`, `invoice.payment_failed`, `customer.subscription.trial_will_end`

### UI Components for Monetization

- **UpgradeBanner**: dismissible, shown at feature limits
- **PlanBadge**: small badge showing current plan
- **TrialCountdown**: days remaining in trial, amber when 3 or fewer
- **PaywallModal**: shown on locked features, explains what they unlock
- **PricingTable**: shared between landing page and in-app billing

---

## 12. Design System

### Colors

```
Primary:       #0F1B2D  Deep Navy (backgrounds)
Navy 800:      #1A2942  Elevated surfaces
Navy 700:      #253754  Hover states
Accent:        #BFFF00  Electric Lime (CTAs, highlights)
Lime Dark:     #99CC00  Accent hover
Slate 500:     #64748B  Secondary text
Slate 300:     #CBD5E1  Body text on dark
Slate 200:     #E2E8F0  Borders on light
Surface:       #F8FAFC  Light backgrounds
Alert:         #EF4444  Live, errors, fouls
Success:       #22C55E  Positive states
Warning:       #F59E0B  Warnings, trial expiring
```

### Portal-Specific Design Variations

All four portals use the same design system. The differences are in layout, density, and tone.

| Portal | Device | Layout | Density | Tone |
|--------|--------|--------|---------|------|
| Admin | Desktop | Sidebar + main, dashboard-heavy | High density, data tables | Professional, oversight |
| Coach | Desktop | Split panel (video + stats) | Medium density, tool-focused | Functional, efficient |
| Player | Mobile | Bottom tabs, card-based | Low density, big numbers | Cool, personal, motivating |
| Parent | Mobile | Bottom tabs, card-based | Minimal, big visuals | Warm, celebratory, emotional |

**Subtle portal differentiation:**
- Each portal can have a tiny colored indicator in the nav (not a full rebrand, just a hint)
- Admin: standard nav
- Coach: standard nav with "Coach" role label
- Player: slightly more energetic, lime accents used more liberally on personal bests
- Parent: warmest tone, most generous spacing, largest tap targets, most shareable

### Typography

- Headlines: Inter, 700-800 weight
- Body: Inter, 400-500 weight
- Stats/Numbers: JetBrains Mono, 400-700 weight
- Import both from Google Fonts

### Key Rules

- Dark mode default for Admin and Coach portals
- Player and Parent portals: dark mode default but should work well in light mode too (they're on phones in various lighting)
- Lime is an accent, not a background. Use sparingly.
- Stats always in JetBrains Mono
- Video clips play inline on mobile, expand to full-screen on tap
- Every video clip moment should feel instant. No loading spinners on clip playback if possible.
- Sharing is first-class in Player and Parent portals. Every stat card and video clip should have a share action.

### Tailwind Config

```javascript
module.exports = {
  darkMode: 'class',
  theme: {
    extend: {
      colors: {
        navy: { DEFAULT: '#0F1B2D', 800: '#1A2942', 700: '#253754' },
        lime: { DEFAULT: '#BFFF00', dark: '#99CC00', muted: '#BFFF0033' },
        slate: { 50: '#F8FAFC', 100: '#F1F5F9', 200: '#E2E8F0', 300: '#CBD5E1', 500: '#64748B', 700: '#334155', 900: '#0F172A' },
        alert: '#EF4444',
        success: '#22C55E',
        warning: '#F59E0B',
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      fontSize: { stat: ['3.75rem', { lineHeight: '1' }] },
      borderRadius: { sm: '4px', md: '8px', lg: '12px', xl: '16px' },
      animation: { 'pulse-live': 'pulse-live 2s ease-in-out infinite' },
      keyframes: { 'pulse-live': { '0%, 100%': { opacity: '1', transform: 'scale(1)' }, '50%': { opacity: '0.7', transform: 'scale(1.15)' } } },
    },
  },
};
```

---

## 13. Landing Page (/about)

### Core Narrative for the Page

A visitor lands here and within 10 seconds understands:
1. The problem: you can't watch the game AND track stats at the same time
2. The solution: record the game, track stats later from video, frame by frame
3. The magic: click any stat, the video jumps to that play
4. The depth: four portals (coach, player, parent, admin), multi-tracker consensus, homework mode
5. The breadth: 15+ sports, one platform
6. What to do: start free trial

### Section 1: Navigation Bar (sticky)

- Left: SnapStats wordmark ("Snap" in lime, "Stats" in white, Inter ExtraBold)
- Right: "Log In" text link + "START FREE TRIAL" lime CTA button
- Navy background, transparent to solid on scroll
- Mobile: hamburger menu

### Section 2: Hero

- Headline: "Watch the game. Track it later."
- Subhead: "Stop missing the action because you're buried in a clipboard. Just record the game. Upload the video. Then track every stat frame by frame, with pause, rewind, and precision you'd never get live. Click any stat and the video jumps right to that moment. Like magic."
- Primary CTA: "START FREE TRIAL" (lime)
- Secondary CTA: "See How It Works" (ghost, scrolls down)
- Trust line: "No credit card required. 15+ sports supported."
- Visual: Desktop browser mockup showing the split-panel tracking interface (video player left, stat panel right, timeline bar bottom). Dark mode. Fake but realistic data.

### Section 3: Sport Grid

- Label: "EVERY SPORT, ONE PLATFORM"
- Headline: "From water polo to wrestling. And everything in between."
- Grid (4 col desktop, 2 col mobile): Water Polo, Basketball, Football, Soccer, Volleyball, Lacrosse, Field Hockey, Ice Hockey, Baseball, Softball, Wrestling, Tennis, Rugby, Swimming, Track and Field, More Coming
- "More Coming" card: lime border, "Request a sport" CTA
- Below: "New sports added through configuration, not code. If you play it, we can track it."

### Section 4: How It Works

- Label: "HOW IT WORKS"
- Headline: "Record. Upload. Track. Review."
- 4 steps:
  1. "Record the Game" / "Point a camera. Phone, tablet, GoPro, whatever. Just hit record and enjoy the game."
  2. "Upload the Video" / "After the game, upload the footage to SnapStats. Pick your team and roster."
  3. "Track Frame by Frame" / "Pause. Rewind. Log every stat with precision you'd never get live. No more missed plays."
  4. "Click Any Stat, See the Play" / "Every stat is timestamped to the video. Click a goal, an assist, a steal, and the video jumps right to that moment."
- CTA: "START FREE TRIAL"

### Section 5: The Magic Moment (Film Sync)

- Label: "FILM SYNC"
- Headline: "Click a stat. Watch the play. Instantly."
- Body: "This is the part that changes everything. Once your stats are logged against the video, every single entry is linked to the exact frame it happened. See a goal in your stat sheet? Click it. The video jumps to two seconds before that play. Want to review every turnover in the second half? Click through them one by one. No scrubbing. No hunting. No wasted time."
- Visual: Desktop mockup with stat list (one row highlighted in lime) and video player showing paused frame. "Jump to play" indicator connecting the stat row to the video timecode.
- Callout pills: "Pause and rewind" / "Frame-by-frame precision" / "No more missed stats"
- CTA: "START FREE TRIAL"

### Section 6: Video Review Workspace

- Label: "DESKTOP FIRST"
- Headline: "Your film room. Built for precision."
- Body: "SnapStats is designed for a desktop or laptop, where you've got the screen space to see the video and the stat panel side by side. Full keyboard shortcuts. Click-to-tag. Drag to scrub. Pause on any frame. Every tool a coach needs to break down the game without the pressure of doing it live."
- Visual: Wide desktop browser mockup of the tracking interface with labeled callouts
- Feature list: "Keyboard shortcuts for fast tagging" / "Frame-by-frame scrubbing" / "Full-screen video with stat overlay" / "Instant undo on every entry" / "Works in any browser, no install"

### Section 7: Four Portals

**This is a NEW section. Show the four experiences.**

- Label: "ONE GAME, FOUR EXPERIENCES"
- Headline: "Everyone sees what they need. Nothing they don't."
- 4 cards, each with a mockup preview and description:

**Coach Portal (Desktop)**
- "Upload video. Track stats frame by frame. Analyze performance. Plan the next game."
- Desktop mockup thumbnail

**Player Portal (Mobile)**
- "See your stats. Watch your highlights. Track your progression. Get better."
- Phone mockup thumbnail

**Parent Portal (Mobile)**
- "See your child shine. Every stat, every highlight, every big moment on your phone."
- Phone mockup thumbnail

**Admin Portal (Desktop)**
- "Oversee every team, every sport, every coach in your program. One dashboard."
- Desktop mockup thumbnail

### Section 8: Multi-Tracker and Homework

**Another NEW section. This is a major differentiator.**

- Label: "BETTER DATA, BETTER COACHING"
- Headline: "15 trackers are better than one."
- Body: "One person tracking stats will miss things. It's inevitable. SnapStats lets your whole team stat the same game. Players watch the film, log stats as homework, and the system compares every version to produce the most accurate stat layer possible. More trackers, better data. No more garbage in, garbage out."

- Sub-section: "Film Study That Actually Works"
- Body: "Assign games as homework. Players watch the film and track stats on their phone. They see the game from the outside for the first time. They understand why plays worked or didn't. Then they see how their version compares to the coach's. Their game IQ improves, and you get crowd-sourced stat accuracy for free."
- Water polo callout: "One program has 14 JV water polo players statting every game as homework. 15 independent stat layers produce a consensus accuracy no single tracker could match. And the players' game awareness has improved dramatically."
- Visual: A mockup showing a consensus comparison view (entries color-coded green/yellow/red for agree/partial/dispute)
- CTA: "START FREE TRIAL"

### Section 9: Pricing

- Label: "PRICING"
- Headline: "Less than a tournament entry fee."
- Subhead: "Start free. Upgrade when you're ready."
- Monthly / Yearly toggle (yearly shows "Save 28%")

**Starter (Free):** 1 team, 1 sport, 3 games/month, basic tracking. CTA: START FREE TRIAL

**Pro ($29/mo or $249/yr):** Unlimited games, film sync, analytics, player profiles, parent portal, CSV/PDF export, 3 stat trackers. Badge: MOST POPULAR. CTA: START FREE TRIAL

**Program ($79/mo or $699/yr):** Everything in Pro + unlimited teams/sports/trackers, multi-tracker consensus, homework mode, season trends, priority support. CTA: START FREE TRIAL

**Enterprise (Custom):** Everything + SSO, API, white-label, dedicated onboarding. CTA: CONTACT US

- Below: "All plans include 14-day free trial of Pro features. No credit card required."
- Note: Multi-tracker consensus and homework mode are Program tier and above. Highlight this.

### Section 10: Coming Soon (Parents)

- Background: navy-800
- Label: "COMING SOON"
- Headline: "For the parents in the stands."
- Subhead: "We're building features that keep the whole family connected to the game."
- 3 teaser cards:
  1. "Public Player Profiles" / "Showcase your athlete's stats, highlights, and progression. Built for college recruiting."
  2. "Live Game Feed" / "Follow the game in real time from anywhere. See every play as it happens."
  3. "Season Highlight Reels" / "Auto-generated video highlights pulled from your timestamped stats."
- Email capture: "Get Notified" with email input
- Tone: Warm, emotional, parent-focused

### Section 11: Trust Stats

- 4 stat blocks: "15+ Sports" / "4 Portals" / "No Sales Call" / "No Credit Card to Start"
- JetBrains Mono numbers, lime, large
- Below: "Built for coaches, players, and parents who want more from their game data."

### Section 12: Final CTA

- Headline: "Stop missing what matters."
- Subhead: "Record the game. Track it later. Click any stat, see the play. Try SnapStats free for 14 days."
- CTA: "START FREE TRIAL"
- Below: "No credit card required. Cancel anytime."

### Section 13: Footer

- Product: Features, Pricing, Sports, How It Works
- Company: About, Contact (hello@snapstats.app), Blog
- Legal: Privacy Policy, Terms of Service
- Connect: @snapstatsapp on X, Instagram, LinkedIn
- Bottom: copyright 2026 SnapStats

---

## 14. Technical Requirements

### Stack
- Next.js (App Router)
- Supabase (database, auth, storage)
- Tailwind CSS
- Deployed on Netlify

### Routing Structure

```
/about                  → Landing page (public)
/login                  → Login (public)
/signup                 → Signup (public)

/admin                  → Admin portal
/admin/teams            → Team management
/admin/users            → User management
/admin/billing          → Subscription and billing
/admin/analytics        → Program analytics

/coach                  → Coach portal dashboard
/coach/games            → Game list
/coach/games/[id]       → Game detail / review
/coach/games/[id]/track → Stat tracking interface
/coach/games/[id]/homework → Assign homework
/coach/roster           → Roster management
/coach/analytics        → Team analytics
/coach/homework         → Homework dashboard (all assignments)

/player                 → Player portal (mobile)
/player/profile         → My stats and profile
/player/games           → My game history
/player/games/[id]      → My stats for a game + video clips
/player/progression     → Season trends
/player/homework        → Homework assignments
/player/homework/[id]   → Homework tracking interface

/parent                 → Parent portal (mobile)
/parent/child/[id]      → Child's profile
/parent/child/[id]/games → Child's game history
/parent/child/[id]/games/[gameId] → Child's game stats + clips
/parent/child/[id]/season → Season view

/settings               → Account settings (all roles)
/settings/billing       → Billing (admin only)
```

### Auth and Role-Based Routing

- Supabase Auth for login/signup
- After login, redirect user to their portal based on role
- Users with multiple roles (e.g., a coach who is also a parent) get a role switcher in the nav
- Middleware checks role permissions on every route
- Unauthorized access redirects to the correct portal, not a 403 page

### Video Storage

- Game videos stored in Supabase Storage (or S3 via Supabase)
- Thumbnail generation on upload
- Video streaming with range requests for scrubbing
- Clip generation: when a user taps a stat, the system serves a segment of the video (timestamp minus 3 seconds to timestamp plus 3 seconds) rather than loading the full video

### Real-Time Updates

- Supabase Realtime for live updates in the parent portal (when new game stats are published, parent sees notification without refreshing)
- Homework submission status updates in real-time on the coach's dashboard

### Performance

- Landing page: static generation (SSG), zero client-side data fetching
- Portal pages: server-side rendering (SSR) with Supabase server client
- Video playback: lazy load, start streaming on demand
- Stat tracking interface: optimistic updates, save every entry immediately, batch sync if offline
- Mobile portals: skeleton loading states, progressive image loading

### Writing Style in the UI

- Lead with verbs: Track. Review. Share. Upload.
- Short sentences. Active voice.
- Use the child's first name in the parent portal, always.
- Sport language is fine. Tech jargon is not.
- Error messages: say what happened and what to do next.
- Empty states: encouraging, never blank.
- Button labels: 1-2 words.

---

*This is a living document. Update it as the product evolves.*
*Last updated: February 2026*
*SnapStats (snapstats.app) | hello@snapstats.app | @snapstatsapp*
