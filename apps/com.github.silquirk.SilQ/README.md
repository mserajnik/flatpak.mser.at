# Sil-Q

> A computer role-playing game with a strong emphasis on discovery and tactical
> combat

- __Type:__ Game
- __Current version:__ `v1.5.1-beta1`
- __Repository:__
  [https://github.com/sil-quirk/sil-q](https://github.com/sil-quirk/sil-q)

## Installation

```sh
flatpak install flatpak.mser.at com.github.silquirk.SilQ
```

## Additional information

### Using the X11 frontend

When using the X11 frontend (`sil-q -mx11`), Sil-Q (like Angband) by default
tries to use the `10x20` font, which is part of
[X.org misc fonts][xorg-misc-fonts]. You should be able to install these fonts
via your distribution's package manager; e.g., if you are on Arch Linux, you
can install the package [`xorg-fonts-misc`][xorg-fonts-misc-package-arch], on
Fedora you can install [`xorg-x11-fonts-misc`][xorg-fonts-misc-package-fedora].

If Sil-Q can't load the font it will exit with an error when trying to launch:

```console
$ flatpak run com.github.silquirk.SilQ
sil-q: Couldn't load the requested font. (10x20)
```

You can also instruct Sil-Q to use a different font. However, since it utilizes
the old [X Logical Font Description][x-logical-font-description] system, this
is a bit more involved: follow the guide in [this thread][install-fonts-thread]
to install the font you want to use. Depending on how you install the font, you
might or might not have to run `mkfontscale` and `mkfontdir` manually (since
your package manager might not do this for you). Ignore step six from the guide
as the environment variable is specific to Angband (Sil-Q uses a different one)
and we need to set this up a bit differently due to the usage of Flatpak.

After installing the font and figuring out its XLFD font name, you can use the
`flatpak override` command to set the `SIL_X11_FONT` environment variable and
thus let Sil-Q know which font you want it to use:

```sh
flatpak override --env=SIL_X11_FONT="-misc-liberation mono-medium-r-normal--20-0-0-0-m-0-iso8859-1" com.github.silquirk.SilQ
```

If you want to set a different font per user, add the `--user` flag to the
`flatpak override` command:

```sh
flatpak override --user --env=SIL_X11_FONT="-misc-liberation mono-medium-r-normal--20-0-0-0-m-0-iso8859-1" com.github.silquirk.SilQ
```

`SIL_X11_FONT` sets the font for all of Sil-Q's windows at once. Sil-Q also
supports per-window environment variables that take precedence over it, so you
can give each window its own font, size and position (window `0` is the main
window, `1` the inventory, `2` the equipment, `3` the combat rolls and `4` the
monster recall):

- `SIL_X11_FONT_<n>`: the font for window `<n>` (e.g., `SIL_X11_FONT_0` for the
  main window only)
- `SIL_X11_COLS_<n>` / `SIL_X11_ROWS_<n>`: the size of window `<n>` in columns
  and rows
- `SIL_X11_AT_X_<n>` / `SIL_X11_AT_Y_<n>`: the position of window `<n>` in
  pixels

These are set the same way as `SIL_X11_FONT` above, via
`flatpak override --env=...`.

If you are using KDE Plasma (e.g., when using Desktop Mode on the Steam Deck),
you should also be able to use the [Hack font][hack-font] out of the box, since
Plasma uses it as its default monospace font:

```sh
flatpak override --env=SIL_X11_FONT="-misc-hack-medium-r-normal--0-0-0-0-m-0-iso8859-1" com.github.silquirk.SilQ
```

### Savegames

Savegames will be stored in
`~/.var/app/com.github.silquirk.SilQ/.sil/Sil-Q/save`.

### Icon

The application icon is a cropped detail of John Howe's painting of the duel
between Fingolfin and Morgoth, the same painting that appears on the cover of
Sil-Q's manual. It is reused here, in that spirit, only to identify the
packaged game; the artwork remains the copyright of John Howe and will be
removed on request. See [`LicenseRef-Sil-Q-icon`][license-sil-q-icon] for
details.

[hack-font]: https://sourcefoundry.org/hack/
[install-fonts-thread]: https://web.archive.org/web/20231028092158/http://angband.oook.cz/forum/showthread.php?t=7336
[license-sil-q-icon]: ../../LICENSES/LicenseRef-Sil-Q-icon.txt
[x-logical-font-description]: https://wiki.archlinux.org/title/X_Logical_Font_Description
[xorg-fonts-misc-package-arch]: https://archlinux.org/packages/extra/any/xorg-fonts-misc/
[xorg-fonts-misc-package-fedora]: https://packages.fedoraproject.org/pkgs/xorg-x11-fonts/xorg-x11-fonts-misc/
[xorg-misc-fonts]: https://gitlab.freedesktop.org/xorg/font/misc-misc
