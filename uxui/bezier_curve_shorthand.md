  cubic-bezier(x1, y1, x2, y2)
               │   │   │   │
               │   │   │   └─ where it ends up (1 = target, >1 = overshoot at end)
               │   │   └───── how quickly it decelerates (lower = snappier stop)
               │   └───────── how far it overshoots (>1 = past target, 1 = exactly there)
               └───────────── how fast it starts (lower = more immediate)
