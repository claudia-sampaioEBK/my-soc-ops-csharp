# SocOps Project Guidelines

## Pre-commit Checklist

Before finalizing any change, run all three steps and fix failures before continuing:

```bash
dotnet build SocOps/SocOps.csproj          # 1. Build — must produce 0 errors
dotnet format SocOps/SocOps.csproj --verify-no-changes  # 2. Lint — fix with: dotnet format
dotnet test                                 # 3. Test — must pass (add tests for new logic)
```

## Architecture

Blazor WebAssembly (.NET 10), client-side only. Key folders:

| Folder | Purpose |
|---|---|
| `Components/` | UI: `BingoBoard`, `BingoSquare`, `GameScreen`, `StartScreen`, `BingoModal` |
| `Services/` | `BingoGameService` (state + `localStorage`) · `BingoLogicService` (static, pure) |
| `Models/` | `BingoSquareData`, `BingoLine`, `GameState` (`Start | Playing | Bingo`) |
| `Data/Questions.cs` | Question bank — append here to add prompts |

`BingoGameService` owns state and raises `OnStateChanged`. Components subscribe to re-render. `BingoLogicService` is stateless (all static). localStorage key: `"bingo-game-state"` v1.

## Conventions

- Nullable reference types enabled — annotate accordingly.
- Component params: `[Parameter]`; callbacks: `EventCallback<T>`.
- Fire-and-forget: `_ = SomeAsync();`
- Board is a flat `List<BingoSquareData>` (25 items); index `12` is always the free space.
- Styling: custom utility classes from `wwwroot/css/app.css` only — not Tailwind CDN. See `.github/instructions/css-utilities.instructions.md`.

## References

- CSS utilities: `.github/instructions/css-utilities.instructions.md`
- Frontend patterns: `.github/instructions/frontend-design.instructions.md`
- Workshop: `workshop/00-overview.md`
