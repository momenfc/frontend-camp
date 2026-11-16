Leak	Retainer chain                                                      Fix
1		GC Roots → Global Context → openedPanels → Array → Detached Panel	استبدال Array بـ numeric counter
2		GC Roots -> DOMTimer -> V8Function -> Context / scope               Add clearInterval
3		GC Roots -> EventListener -> sizeLabelinsystem / Context / scope    Add remove event listener

Final Heap size is 42mb