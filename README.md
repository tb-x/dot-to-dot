# Dot-to-Dot

A maker for printable dot-to-dot puzzles for young kids (around age 5). Each puzzle is a hidden picture drawn as
numbered dots: the child joins them in order with a pencil, and a fish, a rocket or a teddy bear appears. It's
counting practice, and with the numbers going up in 2s, 5s or 10s it's skip-counting practice for bigger kids.
The sheets have no words, so they work for kids who can't read yet, and they're made for a black-and-white
printer. The answer is hidden in a QR code: scan it with a phone camera to watch the picture being drawn.

Live at **https://tb-x.github.io/dot-to-dot/**

## How it plays

- Print a sheet. Start at the dot with the little star around it (number 1).
- Draw a straight line to dot 2, then 3, and so on. The numbers sit just outside the picture, each next to its
  own dot.
- The last dot is already joined back to the star with a dashed line: go over it to close the picture.
- A few lines are printed from the start (an eye, a window, a smile). They don't give the picture away, but
  they make it look finished once the dots are joined. Then it's ready to colour in.
- Scan the QR code at the top right of the puzzle. The answer page shows the dots, draws the line joining them
  in order, then colours the picture in. Tap the picture to draw it again.

## The maker page

- **Dots**: 10, 15, 20, 30 or 50 dots in each picture. 10 to 20 is right for a 5-year-old; the numbers are small
  and printed in light grey (about 3 mm tall up to 20 dots, smaller with more), so the picture stands out.
- **Count by**: 1, 2, 3… for counting, or 2, 4, 6…, 5, 10, 15… and 10, 20, 30… for skip counting.
- **Picture**: Surprise me (a random picture, different ones on the same page) or one of the pictures below.
  Some pictures need more dots to look right, so they're greyed out when there are too few.
- **Per page**: 1 or 2 puzzles (one above the other) on each A4 page.
- **Pages**: how many pages to print at once (up to 20).
- **New pictures** picks new pictures for every page, ↻ on a page picks different ones for that page only, and
  **Print** prints them. Changing the dots or the counting keeps the same pictures. The settings are remembered
  in this browser.
- Clicking a QR code on screen opens its answer page.

The dots are picked from each picture's outline by the computer: it samples the outline finely, then keeps the
points that matter most for the shape (Visvalingam–Whyatt simplification, so corners stay), and spaces out the
dots along straight edges. The numbers go just outside the outline, at whichever spot keeps them clear of the
other numbers, the dots, the printed lines and the line the child will draw.

The QR code holds only the picture, the number of dots and what the numbers count by, e.g. `#p3n20s1` (the
fish, 20 dots, counting in 1s); the answer page works the dots out again the same way. Nothing is stored
anywhere, so a printed sheet keeps working for as long as this page is online. The QR always points at the
published page on GitHub Pages, even when the maker runs on a local server.

## The pictures

| # | Picture | Fewest dots |
| --- | --- | --- |
| 0 | Star | 10 |
| 1 | Heart | 10 |
| 2 | House | 10 |
| 3 | Fish | 10 |
| 4 | Sailboat | 10 |
| 5 | Rocket | 15 |
| 6 | Crown | 10 |
| 7 | Christmas tree | 15 |
| 8 | Apple | 10 |
| 9 | Cat | 15 |
| 10 | Butterfly | 20 |
| 11 | Umbrella | 10 |
| 12 | Whale | 15 |
| 13 | Bird | 15 |
| 14 | Car | 15 |
| 15 | Teddy bear | 15 |
| 16 | Dinosaur | 20 |
| 17 | Bunny | 15 |
| 18 | Elephant | 20 |

The number is the `p` in the answer link, so new pictures only ever go on the end of the list.

## Running it

It's a single `index.html` with no build step. Serve the folder and open it:

```bash
python -m http.server 5220
```

Then go to http://localhost:5220/. Opening `index.html` straight from disk works too. The QR codes are made
by [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4 (MIT), loaded from cdnjs.

After the first visit the page also works offline and can be added to a phone's Home Screen.

## Tuning knobs

Named constants at the top of the script in `index.html`:

| Constant | Default | What it does |
| --- | --- | --- |
| `DEFAULTS` | 20 dots, counting in 1s, Surprise me, 1 a page, 1 page | Starting settings |
| `DOTS` | 10, 15, 20, 30, 50 | The choices in the Dots list |
| `STEPS` | 1, 2, 5, 10 | The choices under "Count by" |
| `SHEETS_MAX` | 20 | Most pages printed at once |
| `GRID` | 1, 2 (one above the other) | How the puzzles sit on a page |
| `DIGITS` | 3.6 / 3.4 / 3.2 / 2.9 / 2.5 mm | How tall the numbers' digits are at 10 / 15 / 20 / 30 / 50 dots, 1 a page |
| `DIGITS_2UP`, `DIGITS_MIN` | 0.85, 2.8 mm | Numbers a bit smaller with 2 a page, but never under 2.8 mm at 20 dots or fewer |
| `NUM_INK` | `#8d93a1` | The numbers' grey: lighter than the dots, so the picture stands out more than the numbers |
| `DOT_R` / `START_R` | 1.15 / 3.4 mm | Size of a dot, and of the star around dot 1 |
| `LINE` | 0.75 mm | Thickness of the lines printed from the start |
| `MAX_PIC` | 168 mm | The biggest a picture gets |
| `QR` | 20 mm | Size of the answer QR code |
| `LEN_W` | 0.06 | Picking dots: higher spreads them more evenly, lower keeps more small bends |
| `CORNER_BONUS` | 3 | Picking dots: how much more a sharp corner counts than a gentle bend |
| `RELAX` | 6 | Picking dots: rounds of evening out the gaps along straight edges |
| `PUBLIC_URL` | `https://tb-x.github.io/dot-to-dot/` | Where the QR codes point |

Changing `LEN_W`, `CORNER_BONUS` or `RELAX` moves the dots, so a sheet printed before the change no longer
matches its answer page exactly (the picture is the same, but the dots sit in slightly different places).
