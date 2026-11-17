# About this fork

This is Nick's personal fork of [Offline Companions Reborn](https://github.com/MaddhattrRocks/Offline-Companions-Reborn)
by Maddhattr. Our changes live on `main`; the author's code is the `upstream` remote.

## How it is installed

- The original stays installed through Thunderstore Mod Manager (profile `Default`) but is **disabled** there.
  Thunderstore keeps updating it; that is how we notice new versions.
- The fork is listed in Thunderstore as `Offline_Companions_Reborn_Fork` (author "Unknown"), added once
  with "Import local mod". Its folder is `BepInEx\plugins\Unknown-Offline_Companions_Reborn_Fork`.
- `dotnet build` copies the new `Companions.dll` into that folder (set by `Environment.props`, which is
  local and not committed). No re-import is needed. While the fork is disabled in Thunderstore
  (its DLL is renamed `Companions.dll.old`), the build skips the copy so it doesn't re-enable it.
- The version Thunderstore shows (1.5.8) comes from the import and does not change with builds.
- The fork keeps the original's plugin GUID (`Maddhattr.OfflineCompanionsReborn`), so it uses the same
  config file and save data. If both copies are ever enabled, BepInEx loads only one of them.
- The BepInEx log (`BepInEx\LogOutput.log`) shows a `[FORK]` line when the fork is the one running.

## Our changes

Keep this list current. Each entry: what it does, and the files it touches.

- Fork marker log line — `src/Companions/Core/CompanionsPlugin.cs` (one line in `Awake`).

## Merging a new upstream version

```
git fetch upstream
git merge upstream/main          # resolve conflicts, keeping both the author's change and ours
dotnet build -c Release          # builds and copies Companions.dll into the fork folder
git push origin main
```

`Translations\` and `speech.json` are not in the repo: the mod writes them next to its DLL on first run.
The fork folder started with copies from the original's folder. Then test in game and check the log for the
`[FORK]` line.
