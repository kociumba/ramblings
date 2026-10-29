---
publish: "true"
created: 2026-06-20T10:53:54.340Z
modified: 2026-10-29T01:01:14.000Z
published: 2026-10-29T01:01:14.000Z
topic difficulty: moderate
---

These are generally a good pattern that i rarely utilize, cause i simply forget to, and keep writing procedural code

This is somewhat of a counter to [[objects]], but it should be treated more as a supplement or alternative to it

```cpp
void (*draw)(const vec2& pos);

int main() {
	draw = draw_circle;
	draw(pos);
	
	draw = draw_rectangle;
	draw(pos)
	
	return 0;
}
```

You can take this further and have some kind of builder for functions

```cpp
using draw_t = void (*)(const vec2& pos);
draw_t draw;

void get_draw(draw_t func) {
	switch(render_state) {
		case CIRCLE:
			func = draw_circle;
			return;
		case RECTANGLE:
			func = draw_rectangle;
			return;
		case CUSTOM:
			func = [](const vec2& pos) {...}
			return
	}
	
	return;
}

int main() {
	get_draw(draw);
	draw(pos);
	
	render_state = RECTANGLE;
	
	get_draw(draw);
	draw(pos)
	
	return 0;
}
```

This can also be more efficiently tackled using lookup tables, somethin like:

```cpp
using draw_t = void (*)(const vec2& pos);
enum RenderState { CIRCLE, RECTANGLE, COUNT };

constexpr draw_t draws[COUNT] = { draw_circle, draw_rectangle };

int main() {
	draws[CIRCLE](pos);
	
	draws[RECTANGLE](pos);
	
	return 0;
}
```
