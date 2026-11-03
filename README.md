# Mikrotik WinBox Flatpak

Flatpak packaging for [WinBox](https://mikrotik.com/winbox), MikroTik's RouterOS
administration tool.

## Building and linting

Install Flatpak Builder if needed:

```sh
flatpak install -y flathub org.flatpak.Builder
```

Build with AppStream screenshot mirroring enabled. This rewrites the compiled
AppStream catalogue's screenshot URLs to `https://dl.flathub.org/media`; without
these flags, `flatpak-builder-lint` reports `appstream-external-screenshot-url`.

```sh
flatpak run --command=flatpak-builder org.flatpak.Builder \
  --force-clean --repo=repo \
  --compose-url-policy=full \
  --mirror-screenshots-url=https://dl.flathub.org/media \
  build-dir com.mikrotik.WinBox.yml
```

Then run the linter against the manifest, metainfo, build directory, and
exported repository:

```sh
flatpak run --command=flatpak-builder-lint org.flatpak.Builder manifest com.mikrotik.WinBox.yml
flatpak run --command=flatpak-builder-lint org.flatpak.Builder appstream com.mikrotik.WinBox.metainfo.xml
flatpak run --command=flatpak-builder-lint org.flatpak.Builder builddir build-dir
flatpak run --command=flatpak-builder-lint org.flatpak.Builder repo repo
```
