build-lists: true

# [fit] Library
# [fit] Oriented
# **Programming**

---

## **@jspahrsummers**

### ReactiveCocoa
### Carthage
### Mantle
### libextobjc

^ Currently at Facebook, and formerly GitHub, but you may know me better from one of these projects.

---

# **What is**
# [fit] coupling?

^ Let's talk about coupling. If two things are _coupled_, they are combined/smashed together in a way that's hard to separate.

---

# [fit] Coupling
# **is a kind of**
# [fit] complexity

^ Complexity is the opposite of simplicity. Something simple is as decoupled as possible.

---

# [fit] Coupling is easy
# [fit] **in the same codebase**

^ There's less barrier to depending on something else in the same codebase.

---

## **Libraries introduce**
# [fit] boundaries

^ It's not impossible, but it is harder to couple your application to the implementation details of a library.

---

## **Libraries introduce**
# [fit] good friction

^ This might seem counter-intuitive, but I think libraries are a good way to force yourself to think more about the abstractions, versioning, etc. It creates a mindset of maintainability.

---

# [fit] **Libraries**
# [fit] simplify

---

## What is
# [fit] **"Library-Oriented"**
## Programming?

^ Creating libraries as frequently as possible.

---

# **One**
# [fit] library
# [fit] concept
# [fit] abstraction

^ Each library should represent exactly one idea/concept/solution/abstraction. If it starts to represent more, split them out!

^ Why?

---

# Simple

^ Fewer concerns = simpler.

---

# Encapsulated

^ If you represent exactly one abstraction, you can encapsulate all of its messy details, and only expose the actually abstracted bits to a consumer.

---

# Maintainable

^ This mostly follows from the previous two points, but it's worth emphasizing that smaller, simpler, and better encapsulated libraries are easier to maintain than monolithic codebases.

---

# [fit] Library
# [fit] **design**

^ It's not enough to just split your codebase into libraries and call it a day. Libraries need to be designed well to be successful.

---

# [fit] Library
# **vs.**
# [fit] Framework

^ First, figure out whether you're building a library or building a framework.

^ In the design sense, not the Cocoa/Apple toolchain sense.

^ "You call a library, but a framework calls you."

---

# [fit] **Base classes are**
# [fit] fragile

^ Case study: Mantle (MTLModel)

^ Fragile base class problem

^ Sometimes consumers need to inherit from other things (e.g. NSManagedObject, UIViewController, etc.)

---

# [fit] **Use** protocols

^ Protocols and composition can replace most needs for inheritance.

---

# [fit] **Use** access control
# [fit] `public`
# [fit] `protected`
# [fit] `private`

^ In Swift, access control keywords can help make public APIs clearer, and hide messy implementation details from consumers.

---

# **One**
# [fit] `final`
# **word**

^ Use final anywhere you haven't explicitly committed to supporting inheritance. Otherwise, bugs may result!

---

# **Match**
# [fit] conventions

^ Especially Apple's. Make your library look like it belongs.

^ There are exceptions (ReactiveCocoa). Different things should be different.

---

# [fit] Dependency
# [fit] **management** :scream:

---

# Xcode Workspace & Git Submodules

- Already installed
- Hard to manage
- …

^ Talk about subtrees too.

---

# CocoaPods

- Widely used
- “Love it or hate it”
- Centrally managed
- Ignores Xcode project configuration
- …

^ Still, always provide an Xcode project!

---

# Carthage

- I helped write it
- Builds upon standard Xcode projects
- Can download prebuilt binaries
- …

---

# Not mutually exclusive

^ Carthage can manage Git submodules. The presence of an Xcode project (used by Carthage) doesn't prevent CocoaPods from working. You don't even need to provide the podspec in the repo.

---

# **Open source**
# [fit] success

^ So you want to release your library as open source. Here are some other things that might be important to its success.

---

# Use in a **real** project

^ ASAP. Avoid open sourcing something that you aren't using yourself!

---

# **Empower** contributors

^ They're your most important community, because they have a vested interest in the project, and they want to help! They can carry on the project even if you can't spend as much time on it.

---

# **Answer** questions

^ Whether on Stack Overflow or GitHub Issues, getting a question answered directly by one of the maintainers is awesome.

---

# Build outward
# **(not inward)**

^ Encourage people to build _on_ your library instead of _in_ it. Creates a richer ecosystem, reduces maintenance burden.

---

# Get to 1.0

^ To many people, it's not "real" until it's 1.0.

---

# [fit] Get to 1.0!

^ It bears repeating! 1.0 also means that you will be introducing fewer breaking changes. Your users care about that.

---

**Thanks to Simon Whitaker, Nacho Soto, and you!**

# Questions?
