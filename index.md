# DuelLingo Privacy Policy

_Last updated: April 24, 2026_

DuelLingo is designed to respect your data. Most of your progress lives only on your device, and the multiplayer features use Apple's CloudKit so your data stays inside your iCloud account.

## What stays on your device

- Your learning progress, stats, streaks, review history, word-mastery list, heat-map activity, and daily quests.
- Your avatar, color, and customized stat selections.
- Your saved friends list (device-scoped cache of the multiplayer profiles you've added).
- Your list of blocked users (device-scoped cache of server-side Block records — see "Moderation" below).

This data lives in SwiftData on your phone. It is not uploaded to any server we control.

## What goes into CloudKit (Apple's iCloud storage)

When you sign in and use multiplayer, the app stores a small amount of data in Apple's CloudKit public database — the same container the app uses to connect players to each other. You can think of this as the "shared space" where DuelLingo players find each other.

**Your public multiplayer profile** (`PlayerProfile` record). Contains:
- Your chosen display handle + 4-digit discriminator (e.g., `jiwoo#1234`).
- Your avatar emoji or photo (whichever you set in-app).
- Your color accent.
- Your current ELO, rank, level, gems, wins, losses, streak, best combo, and aggregate stats — denormalized so friends can render your profile without extra lookups.
- Your Sign-in-with-Apple user identifier — stored so that if you reinstall the app, we can restore your account to the same profile. Not shared with other players.
- A `lastActive` timestamp bumped every ~25 seconds while the app is foreground, so friends can see an "online" dot.

**Friend requests** (`FriendRequest` record). Contains:
- The requesting and receiving users' Apple-assigned CloudKit user IDs.
- Both users' display fields (handle, discriminator, display name, avatar, color) at request time.
- Status (pending / accepted / rejected) and timestamps.

**Async and ranked duel state** (`AsyncMatch`, `RankedMatch` records). Contains:
- Both participants' CloudKit user IDs.
- Both participants' display fields.
- Gameplay state: turn pointer, HP, current round, answer history for the match, outcome when finished.
- Gem balances snapshotted at each turn for settlement.

**Ranked match history** (`RankedMatchHistory` record, one row per match per participant). Contains:
- Your CloudKit user ID.
- The opponent's display fields (not their user ID).
- ELO delta, post-ELO, post-rank, rounds won, rounds total, and when the match was played.

**Ranked matchmaking queue** (`RankedQueue` record). Written only when you are actively looking for a ranked opponent. Contains your CloudKit user ID, ELO, and display fields. Auto-expires after ~30 seconds of inactivity.

## Moderation: Block + Report

DuelLingo includes user-to-user moderation so you can protect yourself from abusive or harassing users.

**Blocking** a user writes a `Block` record to CloudKit containing your CloudKit user ID, the blocked user's CloudKit user ID, and a snapshot of their display handle and avatar at block time. Blocked users stop appearing in your friends list, friend requests, and leaderboards. We mirror the block list to your device so this filtering works instantly. Blocking is one-way; the blocked user is not notified.

**Reporting** a user writes a `Report` record to CloudKit containing your CloudKit user ID, the reported user's CloudKit user ID, their display fields, the reason you selected (harassment, inappropriate handle, inappropriate behavior, spam, or "something else"), the context in the app where you reported from (friends list, friend request, match, etc.), and any optional details you wrote. Reports are retained for moderation review. Reporting is one-way; the reported user is not notified.

## Sign in with Apple

When you sign in with Apple, Apple shares with us only what you choose to share: your Apple user identifier (always), plus optionally your first name and email. We store these locally to personalize onboarding; the user identifier is also stored in CloudKit on your `PlayerProfile` so we can restore your account on reinstall. We do not share these fields with other players.

## Account deletion

You can delete your account from inside the app at any time — Profile → Delete account. Deleting your account:

- Removes your `PlayerProfile` record (including any orphaned profiles tied to the same Apple ID).
- Removes all your sent and received `FriendRequest` records.
- Removes every `AsyncMatch` and `RankedMatch` record you participated in (so your opponent's inbox view of those matches also clears).
- Removes your own `RankedMatchHistory` rows (the opponent's separate row is theirs to delete or keep).
- Removes your `RankedQueue` entry if you were queued.
- Removes all `Block` and `Report` records you authored. Reports about you (where you are the reported party) are retained for moderation.
- Removes all on-device data: profile, review items, friends cache, blocked users cache, saved settings, keychain entries for your Apple user identifier and discriminator.

**Important:** Apple keeps a record of which apps you've signed in to with Apple. After you delete your account in DuelLingo, DuelLingo will still appear in your device's **Settings → Your Apple ID → Sign-In & Security → Apps Using Your Apple ID** list until you tap "Stop Using Apple ID" there. Deleting in-app erases DuelLingo's data; the Settings entry is managed by iOS itself.

## Third-party services

**Google AdMob.** If you see ads in DuelLingo (before purchasing the ad removal), AdMob may collect an advertising identifier and device data depending on your App Tracking Transparency preference. You can change your tracking preference in iOS Settings at any time. We do not control AdMob's data practices directly; see [Google's Ads Privacy Policy](https://policies.google.com/privacy).

**Apple.** Apple processes Sign in with Apple, in-app purchases, CloudKit storage, and push notifications. See Apple's privacy disclosures for details.

## Ad removal

Remove ads with a one-time $2.99 purchase processed by Apple. Apple sends us transaction confirmation only; we never see your payment details.

## Children

DuelLingo is rated 4+ and does not knowingly collect personal information from children under 13. If you believe a child under 13 has created an account, please contact us (below) and we'll remove it.

## Contact

Joseph Rizzo — joseph@winhanced.com

If you have privacy questions, data-deletion requests, or want to report something you saw in the app, that address reaches a real human.
