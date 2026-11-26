# Mind Grid Daily

Mind Grid Daily is a browser puzzle game with five puzzles a day, each testing a different kind of thinking: numerical, verbal, logical, spatial and lateral reasoning. Once the day's five are answered, the game locks and shows a countdown until the next set unlocks at 4pm UK time (based on the player's device clock).

When a player gets a puzzle wrong, they see the correct answer with an explanation, followed by a short skill-builder activity linked to that kind of thinking. As they play, a running IQ-style estimate is updated based on how they perform against each puzzle's difficulty rating.

The question bank holds 365 puzzles per category, enough for a year without repeats. After that it loops back to the start.

## Files

`index.html` is the game itself: layout, styling and logic.

`questions.js` holds every puzzle and skill-builder activity. You can edit it without touching the game code.

Both files must sit in the same folder.

## Running it

Open `index.html` in a browser, or host the folder on any static web host. To publish with GitHub Pages, push both files to a repository, go to Settings, then Pages, choose "Deploy from a branch", select the main branch and the root folder, and save. The game will be live at `https://<your-username>.github.io/<repository-name>/` after a minute or two.

No build step, server or database is needed.

## Editing the questions

Open `questions.js` in any text editor. The `startDate` near the top sets the first puzzle day. Each puzzle day begins at 4pm, so the day starting at 4pm on `startDate` uses the first question in every category, the next day uses the second, and so on. Changing `startDate` restarts the sequence from question one.

Each category (`n` numerical, `v` verbal, `l` logical, `s` spatial, `x` lateral) has a `questions` list and a `drills` list. A question looks like this:

```js
{"q": "2, 6, 12, 20, 30, ?", "options": ["40", "42", "44", "36"], "answer": "42", "level": 110, "explain": "Each term is n × (n + 1), so the next is 6 × 7 = 42."},
```

`q` is the question text. `options` must contain exactly four choices; they are shuffled on screen, so their order in the file doesn't matter. `answer` must match one of the options exactly, including capital letters. `level` is the difficulty on an IQ-style scale, roughly 100 for easy, 115 for moderate, 125 for tough and 135 or above for fiendish, and it feeds the IQ estimate. `explain` is shown after the player answers.

A drill is a list of three pieces of text: the practice task, the answer revealed when the player asks for it, and a technique tip:

```js
["Find the next term: 2, 6, 18, 54, ?", "162. Each term is multiplied by 3.", "When differences grow fast, try ratios instead."],
```

Lists can be any length and do not need to match each other. A category with fewer than 365 questions simply repeats sooner.

Keep the commas between items and the quote marks around text. If the game shows a message saying the question bank could not load, a missing comma or quote mark in `questions.js` is the usual cause. Pasting the file into an online JavaScript checker will point to the line.

## How the IQ estimate works

The estimate starts at 100. After each answer it moves up or down depending on whether the answer was right and how difficult the puzzle was rated, with smaller adjustments as more puzzles are answered. The margin of error shown beside it shrinks over time.

This is an approximation for motivation and fun. The difficulty ratings are set by judgement rather than tested on real players, so the figure is not a validated IQ score and should not be presented as one.

## Saving and limitations

Progress, the daily lock and statistics are stored in the player's browser using local storage. That means progress does not carry across devices or browsers, and clearing browser data resets it and lets the player replay the current day. Players on different devices will see the same puzzles on the same day, because the choice depends only on the date.

## Credits

Built with Claude (Anthropic). Most of the question bank was generated from templates and spot-checked, with a smaller set written by hand. Please report or correct any puzzle that seems wrong by editing `questions.js`.
