# Khel Club Frontend — Walkover Support

This is the Next.js frontend for the Khel Club tournament management system. I updated the referee interface and match fixtures to support Walkover results and display the winning team.

## 1. Referee match screen

The referee match screen is located at:

`src/screen/referee/match/Match.js`

I added a Walkover action that allows the referee to select which team wins when a match is decided by Walkover.

When the referee clicks the button, a dialog opens with the two teams assigned to the match. After selecting a team and confirming, the frontend sends a request to the backend:

`POST /matches/<match_id>/walkover`

The request includes the tournament ID and the selected winning team's ID. If the backend accepts the request, the interface displays a success notification and returns to the referee match list.

The action also respects the match's completion state to help prevent accidental changes to an already completed match.

## 2. Public tournament fixtures

The public fixtures component is located at:

`src/components/fixtures/TournamentFixtures.js`

The fixtures display match information such as the participating teams, round, pool, and match status.

For matches decided by Walkover, the UI displays a `Walkover` badge and highlights the winning team. The winner is identified using `winner_team_id` returned by the backend rather than being inferred from a numeric score.

The existing fixture navigation and Court-wise, Pool-wise, and Status-wise filters should continue to work as before.

## 3. Referee fixture list

The referee fixture list is located at:

`src/components/fixtures/RefereeFixtures.js`

I updated the fixture display to show a Walkover badge and highlight the winning team. This makes it easier for referees to identify matches that have already been decided without opening each match individually.

The fixture data mapping in `src/components/fixtures/BaseFixtures.js` also needs to preserve the match outcome and winner information received from the backend.

## 4. Running locally

Make sure the backend is running before starting the frontend.

Install the dependencies:

```bash
npm install