Leak	Retainer chain                                                      Fix
1		GC Roots → Global Context → openedPanels → Array → Detached Panel	استبدال Array بـ numeric counter
2		GC Roots -> DOMTimer -> V8Function -> Context / scope               Add clearInterval