# Generating Identicons with Faces

⚠️ Warning: This paper is a draft

## Overview, Properties of Hash Algorithms
- Preimage resistance
  - Given a hash value $h$, it should be difficult to find any message $m$ such that $h=\text{hash}(m)$.
- Second preimage resistance
  - Given a specified input $x$, it should be difficult to find another input which produces the same output

### Preimage resistance
Preimage resistance doesn't matter in our case, assuming that public keys are not
considered confidential. We assume that public keys are sent in plaintext, and
that identicons are derived by nodes based on received public keys.

### Second preimage resistance
Second preimage resistance is of critical importance in our case.
Assume that an attacker knows the public key of the server node. The attacker
wants to generate an identicon from that public key such that the resulting identicon
is sufficiently similar to the server's identicon to trick the client node's user agent
into proceeding with a connection to the attacker's node.

What is "sufficiently similar" is dependent on the ability of the client node's user agent to
visually discriminate between two identicon. Further, we believe the ability to visually
discriminate between two identicons is dependent on the specific identicon chosen from its parent set.
A user agent might generate an identicon that is particularly memorable; perhaps it has some shape
or color that the particular user agent associates with something from their (human) memory.

## Chaotic Systems and Time Derivatives
In theory, a chaotic system whose state can be captured at some point
$t$ after an initial time $t=0$ can be used to generate identicons,
in the sense that a chaotic system offers a form of second preimage resistance
for some sufficiently large $t$, and in the sense that some properties or dimensions
of that system can be mapped into a visual representation.

For example, given some seedable fluid dynamics simulator that demonstrates chaotic properties,
for enough timesteps $dt$, you can derive a state. Then you can generate an identicon by
visualizing dimensions of that state (velocity of turbulent flows, angles of vortices, etc.)

## Why Faces?
An identicon should be easy to remember, and it should be easy to distinguish from other identicons in the set.
We believe that humans are more likely to remember the details of a human face than the details of
abstract, geometric shapes. 

This feels intuitive because humans have strong sociological incentives to remember and distinguish between faces,
which in turn informs evolutionary ability. By using faces as identicons, we hack
millions of years of evolution to make it less likely that you'll connect to an incorrect server.

## Constraints for Face Identicons
- Identicons should be constrained in both space and time (deployable on edge)
    - SSH servers are widely deployed on embedded hardware that is resource constrained. For example,
most consumer Wi-Fi access points don't have discrete GPUs.
- Identicons should be renderable in black and white to support old TTYs 
- Identicons should be at most 80 characters wide to accomodate ancient TTYs 

## Implementation
todo: add cool GANs here 👉👈

I like the idea of writing the implementation in C,
then we can compile to WebAssembly using Emscripten

