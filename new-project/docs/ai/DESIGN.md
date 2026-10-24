# Design

<!-- How the product looks and feels. Written from your design sample (Figma, screenshots, Claude design)
     before building UI. Claude Code reads this for every UI task. Keep tokens exact; keep prose short. -->

## Direction
<Mood in 3–5 words, e.g. "dark, bold, sporty, high contrast">. Inspiration: <links or files in docs/design/>.

## Design tokens
| Token | Light | Dark |
|---|---|---|
| --bg | <#F6F6F2> | <#0B0B0C> |
| --surface | <#FFFFFF> | <#16171A> |
| --ink (text) | <#111111> | <#F2F2F2> |
| --accent | <#D4F25A> | <#D4F25A> |
| --danger | <...> | <...> |
- Font: <heading font> / <body font>; sizes <12/14/16/20/28/40>
- Spacing scale: <4, 8, 12, 16, 24, 32, 48>; radius <8 / 16 / 999>
- Breakpoints: phone < 600 px, tablet < 1024 px, desktop ≥ 1024 px

## Screens
| Screen | Route | Who | Main content | Design file |
|---|---|---|---|---|
| Home | `/` | everyone | <hero, lists> | `docs/design/home.png` |
| <...> | <...> | <...> | <...> | <...> |

## Components
<Button (primary/outline/text), Input, Card, Modal/Sheet, Navbar, Footer, Toast, Empty state, Skeleton...>

## Rules
- Mobile first; every screen designed at 390 px and desktop.
- Every data view has loading, empty and error states.
- Accessible: contrast, focus visible, 44 px tap targets, labels.
