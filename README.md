# ZMK Config

This repo contains the [ZMK firmware](https://zmk.dev) configuration files for my [Corne keyboard](https://github.com/foostan/crkbd/), which I purchased from the amazing people at [Typeractive](https://typeractive.xyz/). The keyboard layout is heavily inspired by [Miryoku](https://github.com/manna-harbour/miryoku) with very minor modifications. To deepen my understanding of ZMK, I recreated most of Miryoku's features from scratch, with help from the [ZMK Discord community](https://zmk.dev/community/discord/invite) and Nick Coutsos' beginner friendly [keymap editor](https://nickcoutsos.github.io/keymap-editor/).

## Keymap Features

- Graphite keyboard layout

	I'm using Graphite as the base layer for better typing ergonomics. I also have an `extra` layer with the QWERTY layout.

- Numbers & symbols on base layer

	Since the Corne does not have a dedicated number row, unlike larger boards, I've implemented [combo keys](https://zmk.dev/docs/features/combos) on the base [layer](https://zmk.dev/docs/features/keymaps#layers) for quick access to numbers and symbols. The same numbers and symbols are also available on dedicated layers.

- Caps word & caps lock
 
 	The [Caps word](https://zmk.dev/docs/behaviors/caps-word) key, located on the middle left corner row, triggers caps lock for a single word. This comes in handy when typing environment variables (`STRIPE_SECRET_KEY=123`) and short acronyms (`SQL`, `HTML`, `API`, `NASA`, etc.).

 	There is also an option to toggle the traditional caps lock behavior by pressing `shift` + `caps word`.

 - Sticky shift & sticky hyper

	The [Sticky shift](https://zmk.dev/docs/behaviors/sticky-key) key, located on the bottom left corner row, keeps the shift key pressed until another key is pressed or the 2-second timer elapses (configurable), whichever comes first. It can also be manually toggled off by pressing `sticky shift` again.

- Homerow mods

	[Homerow mods](https://precondition.github.io/home-row-mods) are powerful and convenient, but can be tricky to set up. I've settled on a comfortable configuration that minimizes accidental modifier key activations.

	```c++
	hrm_l: homerow_mods_left {
		compatible = "zmk,behavior-hold-tap";
		label = "HOMEROW_MODS_LEFT_HAND";
		bindings = <&kp>, <&kp>;

		#binding-cells = <2>;
		hold-trigger-key-positions = <6 7 8 9 10 11 18 19 20 21 22 23 30 31 32 33 34 35 39 40 41>;
		tapping-term-ms = <225>;
		flavor = "balanced";
		hold-trigger-on-release;
		quick-tap-ms = <175>;
		require-prior-idle-ms = <130>;
	};

	hrm_r: homerow_mods_right {
		compatible = "zmk,behavior-hold-tap";
		label = "HOMEROW_MODS_RIGHT_HAND";
		bindings = <&kp>, <&kp>;

		#binding-cells = <2>;
		tapping-term-ms = <225>;
		hold-trigger-key-positions = <0 1 2 3 4 5 12 13 14 15 16 17 24 25 26 27 28 29 36 37 38>;
		hold-trigger-on-release;
		flavor = "balanced";
		quick-tap-ms = <175>;
		require-prior-idle-ms = <130>;
	};
	```
	Refer to the [hold-tap](https://zmk.dev/docs/behaviors/hold-tap) docs for detailed explanations of each option.

	In short, if you find yourself accidentally triggering a modifier, consider increasing the tapping term to a range of 200-250ms.
	- `tapping-term-ms = <230>;`

	or changing the hold-tap flavor to tap-preferred: 
	- `flavor = "tap-preferred";`

	For additional guidance:

	> The most important tip I can give is to get into the habit of typing with quick, swift taps. The goal is to reduce the time between press and release to the minimum. Don’t focus on pressing keys, but on tapping keys. -- [precondition](https://precondition.github.io/home-row-mods#quick-swift-taps)


- Extra symbols layer (sym2)

	In addition to Miryoku's stock symbol layer, I've also added a symbol layer labeled `sym2`, inspired by Pascal Getreuer's [Designing a Symbol Layer](https://getreuer.info/posts/keyboards/symbol-layer/index.html). However, maintaining the same symbols across multiple layers adds a lot of mental overhead, which is why this extra layer has largely gone unused. I'm still making changes, looking for ways to merge parts of this layer into the main `sym` layer through the use of combo keys. In the future, I plan on replacing this layer with a [mouse emulation](https://github.com/manna-harbour/miryoku/tree/master/docs/reference#mouse) layer as soon as mouse support is implemented in ZMK.

- Miryoku reference

	The rest of my layout mirrors Miryoku's. Check out the [reference manual](https://github.com/manna-harbour/miryoku/tree/master/docs/reference) for further details.

	---

![](images/zmk_keymap.png)
