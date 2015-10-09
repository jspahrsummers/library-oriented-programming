build-lists: true

# [fit] Library
# [fit] Oriented
# **Programming**

^ Hey, everyone. I'm going to talk today about "library-oriented programming," which is really just an overblown way for me to say "build more libraries!"

^ I've seen a lot of applications that could've been decomposed into libraries, but either the motivation or the knowledge was missing to do it effectively. Hopefully I can provide both of those in this talk.

---

## **@jspahrsummers**

### [ReactiveCocoa][]
### [Carthage][]
### [Mantle][]

^ First, just a little bit about me. My name is Justin Spahr-Summers (@jspahrsummers on Twitter and GitHub).

^ I currently work at Facebook in London, and previously worked at GitHub, but you may know me better from these open source projects that I've contributed to.

---

# [fit] **More** libraries
# [fit] **Less** coupling

^ The main reason I want to promote "library-oriented programming" is because libraries are essential for decoupling your code. This here might as well have been the title of my talk.

---

# **What is**
# [fit] coupling?

^ If two classes/components/whatever are _coupled_, they are combined or smashed together in a way that's hard to separate.

^ For example, UIViewController is highly coupled to UIView. It depends on implementation details of views, and it doesn't make sense to talk about view controllers without talking about views as well.

---

# [fit] Coupling
# **is a kind of**
# [fit] complexity

^ Coupling is bad because it's a kind of complexity. This complexity means you can't understand one class without also understanding all the things that it's coupled to. You can't _test_ the class without also, implicitly, testing all those coupled classes.

^ Simpler code is better code, and decoupling is one way to get there.

---

# [fit] Coupling is easy
# [fit] **in the same codebase**

^ Unfortunately, it's really easy to end up coupling components together when they exist in the same codebase.

^ It starts with a hack here or there ("oh, I just really need to fix this bug, and relying upon this other implementation detail was the easiest way to do it"), until eventually there are hacks upon hacks that prevent you from ever using those components independently again.

---

## **Libraries introduce**
# [fit] boundaries

^ Libraries help here because they more or less _force_ an abstraction boundary on you. What I mean here is that it's _harder_ to couple an application to the implementation details of a library.

^ This is partly because a library has more control over what it exposes. It's also because a library may be updated separately from your application, so you can't depend as strongly on details that may change.

---

## **Libraries introduce**
# [fit] good friction

^ Libraries definitely add a bit of friction to your process, but I think the additional work that's required for a library is a _good thing_, because it forces you to think more about things like versioning, whether you're using the right abstraction, how you're going to handle backwards compatibility, etc.

^ In other words, libraries help create a _mindset of maintainability_.

---

# [fit] **Libraries**
# [fit] simplify

^ Basically, by separating concerns, libraries simplify your code. Even though there might be more work involved, less coupling occurs.

---

## What is
# [fit] **"Library-Oriented"**
## Programming?

^ "Library-oriented" means we should all be thinking about libraries as _early_ as possible in the development process, and create as many as we need to enforce a clean separation of concerns.

^ In library-oriented programming, libraries should be a constant consideration, not just an afterthought.

^ (Graham Lee might have something to say about this terminology later today!)

---

# **One**
# [fit] library
# [fit] concept
# [fit] abstraction

^ To really achieve this mindset, each library should represent exactly _one_ idea/concept/solution/abstraction. If it starts to represent more, split them out!

^ Why?

---

# Simple

^ A library with fewer concerns is inherently simpler.

^ When you try to solve multiple different problems with the same component, the complexity increases—not just linearly, but exponentially! Solving exactly one problem per library keeps your libraries simpler.

---

# Encapsulated

^ When multiple solutions get combined into one, the result is usually a "leaky abstraction," something that tries to cover all these different use cases, but fails to be generic enough to capture them all completely.

^ On the other hand, if you represent exactly one abstraction, you can encapsulate all of its messy details, and only expose a high-level abstraction to the consumer. The result is less leaky, because the problem being solved is smaller and more focused.

---

# Maintainable

^ This mostly follows from the previous two points, but it's worth emphasizing that smaller, simpler, and better encapsulated libraries are easier to maintain than monolithic codebases.

---

# [fit] ~~Base~~
# [fit] ~~Foundation~~
# [fit] ~~Utils~~

^ Finally, never create libraries like these! They just become dumping grounds for stuff, and all that decoupling you did is a lost cause, because then your "Utils" framework gets coupled too.

^ One idea per library.

---

# [fit] **Design**
# [fit] pitfalls

^ It's not enough to just split your codebase into libraries and call it a day. Libraries need to be designed well to be successful.

^ Here are some common pitfalls or problems that I've seen or encountered myself.

---

# [fit] Library
# **vs.**
# [fit] Framework

^ First, figure out whether you're building a library or building a framework.

^ I don't mean what Apple calls a "library" vs. a "framework", but the terms as they relate to API design. "You call a library, but a framework calls you."

^ Libraries are generally simpler and better-encapsulated. I would say: only build a framework if what you want to do cannot be accomplished with a simple library.

---

# [fit] **Base classes are**
# [fit] fragile

^ I made this mistake in Mantle, with the required MTLModel base class. It sucked whenever we would change the implementation, because that could silently break our users' subclasses (this is the "fragile base class problem").

^ And sometimes consumers need to inherit from other things (e.g., UIViewController is unavoidable). With Mantle, we had users that wanted to inherit from NSManagedObject, and that wasn't really supported until Mantle 2.0, when the base class was no longer required.

---

# [fit] **~~Inheritance~~**
# [fit] Protocols

^ Protocols and composition can replace most needs for inheritance.

^ Composition is less fragile, allows you to reuse the behavior of multiple components, and lets users of the library piece things together as _they_ want to—possibly in ways you never even thought of!

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

^ It can be hard to know which dependency managers to support, for users who want to pull in your library.

^ Likewise, if you want to add dependencies to your library itself, there are so many different ways to do it!

^ For example...

---

# Xcode Workspace & Git Submodules

- Always available
- Hard to manage
- Duplicates transitive dependencies
- Doesn’t help with versioning

^ Subtrees have many of these same issues, and make updating or pushing changes upstream more complicated (IMO).

---

# [CocoaPods][]

- Widely used
- “Love it or hate it”
- Centrally managed
- Ignores Xcode project

---

# [Carthage][]

- It’s great (but I’m biased)
- Builds on standard Xcode setup
- Can manage submodules for you
- Prebuilt binaries

---

# Not mutually exclusive

^ A CocoaPods podspec can live alongside an Xcode project. You don't even need to provide the podspec in the repo!

^ If you're adding dependencies to your library, I'd suggest using the lowest common denominator: Git submodules and Xcode. That still leaves the door open for Carthage and CocoaPods, while supporting users that don't want to use either.

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

# [fit] Questions?

# [fit] [github.com/jspahrsummers/library-oriented-programming](https://github.com/jspahrsummers/library-oriented-programming)


[Carthage]: https://github.com/Carthage/Carthage
[CocoaPods]: https://cocoapods.org
[Mantle]: https://github.com/Mantle/Mantle
[ReactiveCocoa]: https://github.com/ReactiveCocoa/ReactiveCocoa
