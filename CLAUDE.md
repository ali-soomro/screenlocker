# screenlocker — Cutefish Screen Locker

## Purpose
Screen locker with user authentication, bundling kcheckpass (from KDE) for password verification via PAM or shadow.

## Build
```bash
cmake -B build -DCMAKE_INSTALL_PREFIX=/usr -DPAM_REQUIRED=ON && cmake --build build && sudo cmake --install build
```

## Dependencies
- Qt6 (Core, DBus, Widgets, Quick, LinguistTools)
- X11
- PAM (optional, enabled by default)

## Structure

### screenlocker/
- `main.cpp` — entry point
- `application.cpp/h` — application logic
- `authenticator.cpp/h` — authentication via kcheckpass
- `qml.qrc` — QML resources
- `qml/LockScreen.qml`, `qml/LoginButton.qml`, `qml/IconButton.qml`, `qml/MprisItem.qml` — UI

### checkpass/
- `checkpass.c`, `checkpass.h` — password verification core
- `checkpass_pam.c` — PAM backend
- `checkpass_shadow.c` — shadow password backend
- `checkpass-enums.h` — enums
- Feature checks: `sys/prctl.h`, `sys/signalfd.h`, ptrace control

## Install Targets
- Binary → `${CMAKE_INSTALL_BINDIR}`
- Translations → `/usr/share/cutefish-screenlocker/translations/`

## Qt5→Qt6 Migration Notes
- Qt5 → Qt6
- `QX11Info` → `QNativeInterface::QX11Application`
- `qAsConst` → `std::as_const`
- `nativeEventFilter` result type: `long int*` → `qintptr*`
- X11 operations guarded with xcb platform checks

## Status
✅ Ported, built, installed, pushed (github.com/ali-soomro)
