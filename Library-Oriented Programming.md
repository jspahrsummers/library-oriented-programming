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

# [fit] Coupling

^ Let's talk about coupling. If two things are _coupled_, they are combined/smashed together in a way that's hard to separate.

---

# [fit] **Coupling**
# is a kind of
# [fit] **Complexity**

^ Complexity is the opposite of simplicity. Something simple is as decoupled as possible.

---

# Coupling is harder **across libraries**

^ You can't couple to libraries' implementation details, for example.

---

# Frameworks and libraries
# [fit] **reduce coupling**

---

# [fit] Library
# [fit] oriented

^ Creating libraries as frequently as possible.

---

# [fit] **One library**
# [fit] per abstraction

---

# Simpler

---

# Encapsulated

---

# Maintainable

---

# When to decompose

^ When is the right time to split out a library/framework?

---

# One library per abstraction

---

# API design

---

# [fit] Library
# vs.
# [fit] Framework

^ In the design sense, not the Cocoa/Apple toolchain sense

---

# Don't provide a base class

^ Case study: Mantle (MTLModel)

---

# Use protocols

---

# Use access control
# (in Swift)

^ Public/protected/private

---

# Match conventions

^ Especially Apple's. Make your library look like it belongs.

^ There are exceptions (ReactiveCocoa). Different things should be different.

---

# [fit] Dependency
# [fit] management

---

# Git Submodules

Pros
Cons

---

# CocoaPods

Pros
Cons

^ Still, always provide an Xcode project!

---

# Carthage

Pros
Cons

^ I'm biased!

---

# Not mutually exclusive!

---

# Ensuring
# [fit] success

---

# Use it in a real project

^ ASAP

---

# Empower contributors

---

# Answer questions

^ Whether on Stack Overflow or GitHub Issues, getting a question answered directly by one of the maintainers is awesome.

---

# Open ecosystem

^ Encourage people to build _on_ your library instead of _in_ it. Creates a richer ecosystem, reduces maintenance burden.

---

# Get to 1.0!

---

# [fit] :zap: ReactiveCocoa 3 :zap:

^ For example

---

# [fit] Questions?
