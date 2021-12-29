#[[excerpt]] [Angular Change Detection Explained | Articles by thoughtram](https://blog.thoughtram.io/angular/2016/02/22/angular-2-change-detection-explained.html)

- tags: #[[SimpRead]]
- read date: [[2021_12_13  ]]
- desc: Wonder how change detection in Angular works?  This article is a write-up of that talk and discusses change detection and tricks to make is super fast.
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888636>)  What’s Change Detection anyways?
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888638>)  What causes change?
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639379173320>)  Basically application state change can be caused by three things:
  
  *   **Events** - `click`, `submit`, …
  *   **XHR** - Fetching data from a remote server
  *   **Timers** - `setTimeout()`, `setInterval()`
  > 会引发change derection的原因，一般有三个：
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888642>)  Who notifies Angular?
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639379325028>)  The short version is, that somewhere in Angular’s source code, there’s this thing called `ApplicationRef`, which listens to `NgZones` `onTurnDone` event. Whenever this event is fired, it executes a `tick()` function which essentially performs change detection.
  
  ```ts
  // ver// very simplified version of actual source
  class ApplicationRef {
  
  changeDetectorRefs:ChangeDetectorRef[] = [];
  
    constructor(private zone: NgZone) {
      this.zone.onTurnDone
        .subscribe(() => this.zone.run(() => this.tick());
    }
  
    tick() {
      this.changeDetectorRefs
        .forEach((ref) => ref.detectChanges());
    }
  }
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888644>)  Change Detection
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888646>)  Performance
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888648>)  Smarter Change Detection
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888649>)  Immutable Objects
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888651>)  Reducing the number of checks
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888653>)  Observables
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888655>)  There’s more…
- [📌](<http://localhost:7029/reading/625?title=Angular Change Detection Explained - Articles by thoughtram#id=1639377888656>)  Credits