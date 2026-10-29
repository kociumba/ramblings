---
publish: "true"
created: 2026-06-20T18:26:11.430Z
modified: 2026-10-28T22:35:06.000Z
published: 2026-10-28T22:35:06.000Z
topic difficulty: beginner
---

### code comments

As a general rule of thumb code comments should be treated as if they are lying.

This is due to constant changes in a codebase, if a codebase is rarely updated or updated with a lot of care this might not be true, but in projects that are still evolving or with a team of people working on them, code comments often look like this:

```cpp
// do_something takes a pointer to Bar
void do_something(Foo* foo) {...}
```

This is of course a manufactured strawman example but similar mistakes and mishaps do happen on regular basis, just ask anyone working on a big codebase with a team

For this reason ==Code should be self documenting==, meaning that reading the code should be simple and tell you what it does

This is another argument against typical "clean code" practices which i touch up on here: [[objects#^code-clutter]]

### doc comments

There is a real difference between [[#code comments]] and [[#doc comments]], well maintained doc comments in a codebase are genuinely very useful, take for example the doc comments from [SDL 3](https://github.com/libsdl-org/SDL):

```c
/**
 * Initialize the SDL library.
 *
 * SDL_Init() simply forwards to calling SDL_InitSubSystem(). Therefore, the
 * two may be used interchangeably. Though for readability of your code
 * SDL_InitSubSystem() might be preferred.
 *
 * The file I/O (for example: SDL_IOFromFile) and threading (SDL_CreateThread)
 * subsystems are initialized by default. Message boxes
 * (SDL_ShowSimpleMessageBox) also attempt to work without initializing the
 * video subsystem, in hopes of being useful in showing an error dialog when
 * SDL_Init fails. You must specifically initialize other subsystems if you
 * use them in your application.
 *
 * Logging (such as SDL_Log) works without initialization, too.
 *
 * `flags` may be any of the following OR'd together:
 *
 * - `SDL_INIT_AUDIO`: audio subsystem; automatically initializes the events
 *   subsystem
 * - `SDL_INIT_VIDEO`: video subsystem; automatically initializes the events
 *   subsystem, should be initialized on the main thread.
 * - `SDL_INIT_JOYSTICK`: joystick subsystem; automatically initializes the
 *   events subsystem
 * - `SDL_INIT_HAPTIC`: haptic (force feedback) subsystem
 * - `SDL_INIT_GAMEPAD`: gamepad subsystem; automatically initializes the
 *   joystick subsystem
 * - `SDL_INIT_EVENTS`: events subsystem
 * - `SDL_INIT_SENSOR`: sensor subsystem; automatically initializes the events
 *   subsystem
 * - `SDL_INIT_CAMERA`: camera subsystem; automatically initializes the events
 *   subsystem
 *
 * Subsystem initialization is ref-counted, you must call SDL_QuitSubSystem()
 * for each SDL_InitSubSystem() to correctly shutdown a subsystem manually (or
 * call SDL_Quit() to force shutdown). If a subsystem is already loaded then
 * this call will increase the ref-count and return.
 *
 * Consider reporting some basic metadata about your application before
 * calling SDL_Init, using either SDL_SetAppMetadata() or
 * SDL_SetAppMetadataProperty().
 *
 * \param flags subsystem initialization flags.
 * \returns true on success or false on failure; call SDL_GetError() for more
 *          information.
 *
 * \threadsafety This function should only be called on the main thread.
 *
 * \since This function is available since SDL 3.2.0.
 *
 * \sa SDL_SetAppMetadata
 * \sa SDL_SetAppMetadataProperty
 * \sa SDL_InitSubSystem
 * \sa SDL_Quit
 * \sa SDL_SetMainReady
 * \sa SDL_WasInit
 */
extern SDL_DECLSPEC bool SDLCALL SDL_Init(SDL_InitFlags flags);
```

Extreme care is taken here to correctly document what the function does, related points of interest are provided, all parameters and returns are stated along with specific information on things like thread safety or version availability

This kind of carefully curated doc comments make the argument from [[#code comments]] null and void as you don't need to see the code to know exactly how to use it

> [!warning]
> This does have a maintenance pitfall unfortunately, if any functionality changes, these need to be manually updated, which can easily cause them to desync from the actual code in which case we are back to [[#code comments]] lying
