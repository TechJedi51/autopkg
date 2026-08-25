# TechJedi51 AutoPkg Recipes

AutoPkg download and Munki recipes maintained by TechJedi51.

The repository currently contains 26 download recipes and 26 corresponding Munki import recipes. Downloaded applications and installer packages are verified with AutoPkg's code-signature processor before import whenever the vendor supplies signed software.

## Requirements

- macOS
- AutoPkg 2.3 or newer
- Munki tools and a configured Munki repository when running `.munki.recipe` files
- Git, so AutoPkg can manage recipe repositories

The recipes use AutoPkg core processors and do not require a separate shared-processor repository.

## Add the repository

```sh
autopkg repo-add TechJedi51/autopkg
```

Confirm that AutoPkg has registered it:

```sh
autopkg list-repos
```

## Create a local override

Do not put organization-specific settings directly in the shared recipes. Create an override and customize its catalog, Munki repository subdirectory, descriptions, or other deployment metadata there.

For example:

```sh
autopkg make-override com.github.techjedi51.munki.iStatMenus7
```

After reviewing an upstream recipe change, update the local override's trust information:

```sh
autopkg verify-trust-info local.munki.iStatMenus7
autopkg update-trust-info local.munki.iStatMenus7
```

## Recipes

| Product | Recipe name | Target | Minimum macOS | Maximum macOS |
| --- | --- | --- | ---: | ---: |
| 8x8 Work | `8x8 Work-Apple Silicon` | Apple silicon | 12.0 | — |
| 8x8 Work | `8x8 Work-Intel` | Intel | 12.0 | — |
| Bartender 5 | `Bartender 5` | Universal | 14.0 | 15.99 |
| Bartender 6 | `Bartender 6` | Universal | 15.0 | 26.99 |
| iStat Menus 7 | `iStat Menus7` | Universal | 11.0 | — |
| iMazing 3 | `iMazing3` | Universal | 10.12 | — |
| MacX YouTube Downloader | `MacX YouTube Downloader` | Universal | 10.13 | — |
| Ecamm Live | `Ecamm Live` | Universal | 11.2 | — |
| Cocktail 16 | `Cocktail16` | Ventura | 13.0 | 13.99 |
| Cocktail 17 | `Cocktail17` | Sonoma | 14.0 | 14.99 |
| Cocktail 18 | `Cocktail18` | Sequoia | 15.0 | 15.99 |
| Cocktail 19 | `Cocktail19` | Tahoe | 26.0 | 26.99 |
| Cocktail 20 | `Cocktail20` | Golden Gate | 27.0 | 27.99 |
| LibreOffice | `LibreOffice-Apple-Silicon` | Apple silicon | 11.0 | — |
| LibreOffice | `LibreOffice-Intel` | Intel | 10.15 | — |
| Lingon Pro 10 | `Lingon Pro` | Universal | 14.0 | — |
| Resilio Sync 3 | `Resilio Sync` | Universal | 10.13 | — |
| OnyX | `OnyX1015` | Catalina | 10.15 | 10.15.99 |
| OnyX | `OnyX11` | Big Sur | 11.0 | 11.99 |
| OnyX | `OnyX12` | Monterey | 12.0 | 12.99 |
| OnyX | `OnyX13` | Ventura | 13.0 | 13.99 |
| OnyX | `OnyX14` | Sonoma | 14.0 | 14.99 |
| OnyX | `OnyX15` | Sequoia | 15.0 | 15.99 |
| OnyX | `OnyX26` | Tahoe | 26.0 | 26.99 |
| OnyX | `OnyX27` | Golden Gate, Apple silicon | 27.0 | 27.99 |
| Zoom Workplace | `zoom.us` | Universal | 10.15 | — |

Each entry has a `.download.recipe` and a `.munki.recipe` file.

## Important notes

### Catalogs

The Munki recipes default to the `testing` catalog. Promote imported items to production catalogs only after testing them in your environment.

### Architecture-specific recipes

8x8 Work and LibreOffice have separate Intel and Apple-silicon recipes. Their Munki metadata contains `supported_architectures` so only compatible clients receive each item.

### OS-specific utilities

Cocktail and OnyX publish separate applications for major macOS releases. Use only the recipe matching the target operating system. Do not deploy an older OnyX edition to a newer macOS release.

### OnyX for macOS 27

The OnyX 27 recipe currently follows Titanium Software's Golden Gate beta download. When Titanium publishes the stable release, verify the vendor's final URL and code signature before changing the recipe from the beta download path.

### Recipe trust

AutoPkg recipe trust protects local overrides from unreviewed parent-recipe changes. A failed trust verification is a prompt to review the upstream diff; it should not be bypassed without understanding the change.

## Testing changes

Check recipe syntax before committing:

```sh
find . -name '*.recipe' -print0 | xargs -0 -n 1 plutil -lint
```

Inspect a recipe chain without importing software:

```sh
autopkg info -p com.github.techjedi51.munki.Bartender6
```

Run a recipe verbosely after configuring `MUNKI_REPO`:

```sh
autopkg run -vv local.munki.Bartender6
```

## License

No open-source license has yet been selected for this repository. Add a `LICENSE` file if these recipes are intended for unrestricted public reuse.
