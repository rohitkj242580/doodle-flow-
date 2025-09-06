# doodle-flow-
A lightweight, touch-first drawing app for Android written in Kotlin — fast sketching, layer-like strokes, undo/redo, export to PNG, and small APK footprint.
Short: Doddle Flow is a simple, elegant drawing app for Android (Kotlin). It focuses on fluid touch drawing, reasonable performance, easy export/share, and a clean, minimal UI — great for quick sketches, annotations, or prototyping gesture features.

Features

Freehand drawing with pressure-like stroke width (velocity-based)

Multiple brushes (pen, marker, eraser) with size selector

Undo / Redo (stroke-based)

Clear canvas

Save & share PNG to gallery

Export with transparent background option

Simple color picker + recent colors

Fast, memory-friendly stroke storage (path + paint model)

Optional grid/background templates

Lightweight: no large dependency heavy frameworks

Screenshots

(add images in /assets or GitHub repo — use screenshots/ folder and reference in README)

Tech stack

Language: Kotlin

Android SDK: AndroidX, minSdk 21+ recommended

Gradle (Kotlin DSL or Groovy)

Optional libs: Material Components, AndroidX Core, Lifecycle, Coroutines (for async saving)


Clone the repo

git clone https://github.com/<your-org>/doddle-flow.git
cd doddle-flow


Open in Android Studio (Arctic Fox or newer), let Gradle sync.

Set required permissions in AndroidManifest.xml:

<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"
    android:maxSdkVersion="28" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />


For Android 10+ use MediaStore APIs and scoped storage (no WRITE_EXTERNAL_STORAGE) — see SaveHelper.kt.

Build & run on an emulator or device.

Core design (how it works)

Stroke model: each stroke saved as { Path, PaintState (color, width, mode), timestamp }. This enables efficient undo/redo by pushing/popping stroke objects.

Rendering: DrawingView draws all strokes into an offscreen bitmap (backing bitmap) for fast redraw and on-demand export.

Input handling: onTouchEvent converts MotionEvents to Path operations; implement smoothing (quadTo) for nicer curves.

Persistence: export writes backing bitmap to PNG through a coroutine; for Android 10+ use MediaStore and ContentResolver.
