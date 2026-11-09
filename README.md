# OPD Follow-Up Calendar

Installable app for an outpatient follow-up schedule: calendar, upcoming table,
NAWC / no-show tiers, discharged / PRN, pending OR, admitted, mortality — plus
editing from the phone (reschedule, add, move between lists, leave and holidays).

## No patient data here

This repository and the GitHub Pages site are **code only**. Pages sites are
public, so the patient list lives in a separate **private** repository and the
app reads and writes it through the GitHub API with a fine-grained token that is
stored on each device. Nothing in this repo should ever contain a name, case
number or diagnosis.

## Install

**iPhone** — open the Pages URL in Safari → Share → Add to Home Screen.
**Mac** — open it in Safari → File → Add to Dock.

First launch asks for a token: GitHub → Settings → Developer settings →
Fine-grained tokens → Generate, with repository access limited to the private
data repo and **Contents: Read and write**. Paste it once per device.

## How edits sync

Each edit is queued on the device, then replayed onto the newest copy of the data
file and committed. If the file changed in between (another device, or a resync
from the Mac), the edit is re-applied to the new version instead of overwriting
it. Offline edits wait in the queue and go out when there is signal.

The data file keeps one record per line so git can merge edits to different
patients.

## Files

| File | |
|---|---|
| `index.html` | the whole app |
| `manifest.webmanifest`, `icon-*.png`, `apple-touch-icon.png` | install metadata |
| `sw.js` | offline cache for the app shell (never the API) |

The Mac-side tool `opdcal.py` builds a read-only offline snapshot of the
calendar from this `index.html` plus the private data file.
