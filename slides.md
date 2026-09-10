---
theme: default
layout: cover
title: "Rust @ Amazon and Amazon @ Rust"
info: |
  RustConf 2026
  Russell Cohen
colorSchema: light
transition: fade
drawings:
  persist: false
duration: 35min
section: intro
---

<div class="title-slide">
  <div class="title-meta">
    <span>RustConf 2026</span>
    <span>Russell Cohen <b>&middot;</b> @rcoh</span>
  </div>

  <div class="title-composition">
    <h1 aria-label="Rust at Amazon and Amazon at Rust">
      <span class="title-line title-line-forward">
        <span class="title-ink">Rust @</span>
        <span class="title-rust">Amazon</span>
      </span>
      <span class="title-and"><i></i><b>and</b><i></i></span>
      <span class="title-line title-line-reverse">
        <span class="title-rust">Amazon @</span>
        <span class="title-ink">Rust</span>
      </span>
    </h1>
  </div>
</div>

<!--
Hello! I'm Russell, I work on Rust at Amazon. Today I want to share 4 new OSS tools and libraries that we use Amazon that you can use immediately.
-->

---
layout: default
class: about-slide
section: intro
---

<AboutSlide />

<!--
First a tiny bit about me. I joined AWS in 2020 to create the AWS SDK for Rust. So, if you have spent 6 minutes waiting for the EC2 SDK to compile, I personally apologies.

Now I work on a much broader objective: Make Rust successful at Amazon.

Rust at Amazon started way before me. When people started using Rust at Amazon, Rust still looked like this:
-->

---
layout: default
class: retro-rust-slide
section: intro
---

```rust {all|2|3|9}
fn greet(
    names: ~[~str],
    count: @int,
) {
    if names.len() == 0 {
        fail!("nobody here")
    }
    for n in names.iter() {
        spawn(proc() println!(
            "hi {}, #{}", *n, *count
        ))
    }
}
```

<!--
When folks at Amazon started using Rust, Rust still looked like this.

[click] You could use tilde to denote boxed pointers.

[click] @ for a garbage-collected pointer.

[click] and `proc()` was a built-in one-shot closure for spawning tasks.
-->

---
layout: default
class: timeline-slide
section: intro
---

<TimelineSlide />

<!--
That was way back in 2014. By 2016 a few intrepid folks had a real build system working.

And then, recently, something changed:

[click]

AI got good at Rust.
-->

---
layout: image
image: /images/langtrends/final-open-tr-light.svg
class: growth-chart-slide
backgroundSize: contain
section: intro
footer: false
---

<!--
Rust's share of Amazon developers is now growing faster than any other major language. 

There has never been a single day in the last 8 years when year-of-year portion of Amazon builders using Rust has gone down.
-->

---
layout: statement
class: so-what-slide
section: intro
---

# So what?

<!--
So what?

Well, there are a lot of people at Amazon writing Rust and a lot of it has turned into OSS libraries you can use.

Here's a lightening round of some that you can use right now
-->

---
layout: default
class: index-slide
section: intro
qrCircle: true
---

# Five things you can use now

<div class="project-index">
  <div><span>01</span><strong>metrique</strong><small>production metrics</small></div>
  <div><span>02</span><strong>dial9</strong><small>runtime traces</small></div>
  <div><span>03</span><strong>Shuttle + Turmoil</strong><small>deterministic simulation testing for everyone</small></div>
  <div><span>04</span><strong>Hydro</strong><small>distributed programs</small></div>
  <div><span>05</span><strong>Battery Packs</strong><small>curated crate sets</small></div>
</div>

<!--
We have metrique, our metrics library, dial9 an always on profiler, shuttle and turmoil for simulation testing, hydro for distributed systems, and Battery Packs for sharing ecosystem knowledge.

[click] The QR code links to all of the projects in the talk.
-->

---
layout: default
class: project-slide metrique-slide
section: metrique
---

<div class="project-number">01</div>

<div class="project-intro">
  <div>
    <h1>metrique</h1>
    <p>High-performance wide-event metrics for Rust.</p>
  </div>
  <a href="https://github.com/awslabs/metrique">github.com/awslabs/metrique</a>
</div>

<!--
First metrique. Amazon does metrics a little bit differently from a lot of other companies. Most teams use "wide event" (aka unit-of-work) metrics. This is where the metrics that you see on a graph don't come from a counter in your code, instead they come from an _event_ your code emits that turns into a counter.
-->

---
layout: default
class: project-slide code-slide
section: metrique
---

<div class="project-eyebrow">01 &middot; metrique</div>

```rust
#[metrics(rename_all = "PascalCase")]
struct RequestMetrics {
    #[metrics(timestamp)]
    timestamp: Timestamp,
    number_of_ducks: usize,
    #[metrics(unit = Millisecond)]
    operation_time: Timer,
    success: bool, // flushes as 0 or 1
}

let mut metrics = RequestMetrics::init();
metrics.number_of_ducks = 5;
metrics.success = true;
// one wide event flushes as the scope drops
```

<MetriqueFormats />

<!--
When the event exists, it makes it much easier to debug why a line on a graph went up.

metrique makes those events plain structs with primitives for timestamps and counters and the sorts of things you would want in metrics. Because everything is "just structs", it is very low overhead.

Metrique decouples your metrics from the format they eventually get emitted to.

[click] Inside of Amazon, we have a metrique formatter for our own gnarly metric format. But the same struct also emits plain JSON, EMF, otel which are all in the Open source repo. Metrique also has pretty format just for local debugging.

So if you have an application that emits metrics, it might be worth a look.
-->

---
layout: default
class: project-slide dial9-slide
section: dial9
---

<div class="project-number">02</div>

<div class="dial9-copy">
  <h1>dial9</h1>
  <p>An always on profiler for production</p>
  <a href="https://dial9-rs.github.io/blog/dial9-a-flight-recorder-for-rust/">dial9-rs.github.io</a>
</div>

<!--
On to dial9; So a quick story; earlier this year, I got pulled into a performance investigation for a team that was onboarding to Rust. To figure out their performance problem, we really needed to pull lots of events from Tokio, in production. Anyway, long story short, turns out, if you run Tokio and also 16k Java threads on the same host it doesn’t work super well.

But along the path of solving this, we build dial9 which is an always-on profiler you can use in production that works especially well with Tokio applications.
-->

---
layout: default
class: project-slide dial9-benchmark-slide dial9-encode-slide
section: dial9
---

<div class="project-eyebrow">02 &middot; dial9</div>

<Dial9Encode />

<!--
Because dial9 was originally built to record every single event coming off of Tokio, it needs to serialize events very efficiently.

Serializing an event in dial9 only takes a 10s of nanoseconds and the events and (slide)
-->

---
layout: default
class: project-slide dial9-benchmark-slide dial9-size-slide
section: dial9
---

<div class="project-eyebrow">02 &middot; dial9</div>

<Dial9Encode mode="gzip" />

<!--
When compressed, events are in the single-digit bytes
-->

---
layout: default
class: project-slide dial9-sources-slide
section: dial9
---

<div class="project-eyebrow">02 &middot; dial9</div>

<Dial9Sources />

<!--
Once you have a system that can record lots of events, very efficiently, it can be the central collector for all sorts of data.

[click] Tokio events,

[click] profiling data,

[click] Linux kernel events,

[click] tracing spans,

[click] metrique metrics,

[click] and any custom events you emit from your application

[click] all end up in the same trace file. Each of these is useful alone, but they are way more useful together.

[click] dial9 can write that trace to S3, local disk, or other destinations. Destination support is built into dial9.
-->

---
layout: image
image: /images/dial9-shot-1.png
class: shot-slide
backgroundSize: contain
section: dial9
---

<!--
And once you have all this data in one place, you can do some pretty cool stuff. For example, you can look at the slowest instance of a particular request, then jump
-->

---
layout: image
image: /images/dial9-shot-2.png
class: shot-slide
backgroundSize: contain
section: dial9
footer: false
---

<!--
directly the the individual poll, and see why it was slow. In our experience with teams using this at AWS and also in the broader Rust community, this ability is really powerful
-->

---
layout: default
class: project-slide testing-slide
section: testing
---

<div class="project-number">03</div>

# Shuttle + Turmoil

<div class="testing-pair">
  <div>
    <strong>Shuttle</strong>
    <span>concurrent schedules</span>
    <a href="https://github.com/awslabs/shuttle">awslabs/shuttle</a>
  </div>
  <div>
    <strong>Turmoil</strong>
    <span>networks and hosts</span>
    <a href="https://github.com/tokio-rs/turmoil">tokio-rs/turmoil</a>
  </div>
</div>

<img src="/images/turmoil.png" alt="The Turmoil GitHub project" class="turmoil-image" />

<!--
So dial9 is like a profiler++++.

Shuttle and Turmoil help you simulate rare failure modes deterministically to catch really hard bugs.

Shuttle is a tool to explore different concurrent schedules of your Rust program. Turmoil lets you do deterministic simulation testing of network faults.

Not _every_ library needs one of these tools, but when you need one, the are extremely helpful.

dial9 uses shuttle to validate our cross threaded event bus maintains certain invariants. S3 uses shuttle to validate that its metadata store works as expected.

I went looking for an example bug caught with shuttle that I could share on a conference talk slide; but the bugs shuttle finds are very complicated and that is kind of the point. Shuttle finds bugs that are only reachable in complex scenarios between interacting threads. If this describes your code, its worth taking a look.
-->

---
layout: default
class: project-slide hydro-slide
section: hydro
---

<div class="project-number">04</div>

<div class="hydro-copy">
  <h1>Hydro</h1>
  <p><strong>One Rust program.</strong><br>Many machines.</p>
  <a href="https://hydro.run/">hydro.run</a>
</div>

<div class="hydro-thesis">
  Correctness and deployment become part of the programming model.
</div>

<!--
Next I want to talk about Hydro which is a joint work from AWS and Berkeley.

 we have a bunch of the Hydro maintainers with us at RustConf this week, go say hi!

 Rust makes it way safer to write really fast code while ruling out huge classes of memory and concurrency bugs.

Hydro does the same thing for distributed systems.
-->

---
layout: default
class: project-slide hydro-code-slide
section: hydro
---

<HydroCode />

<!--
In Hydro, the way you express your system makes it possible to rule out classes of bugs that can exist in distributed systems.
-->

---
layout: default
class: project-slide hydro-raft-slide
section: hydro
---

<HydroRaft />

<!--
I want to share a quick anecdote about the sorts of problems Hydro can catch.

[click]

Most folks are probably familiar with the Raft consensus protocol. It is a theoretically simpler and easier to understand alternative to Paxos.

[click]

An early version of Raft actually had a potentially severe bug that went undetected for some time.

[click]

You can use tools like Hydro to implement consensus protocols like Paxos and Raft. If you implement the buggy version of Raft with Hydro, Hydro's built-in simulation tests catch it immediately.

Sources:
- https://raft.github.io/
- https://groups.google.com/g/raft-dev/c/t4xj6dJTP6E/m/d2D9LrWRza8J
-->

---
layout: default
class: project-slide battery-pack-slide
section: battery
---

<BatteryPackIntro />

<!--
One last thing. These are a lot of libraries; how do I figure out what to use? how do I actually use them?

Using Rust well requires a lot of tacit ecosystem knowledge: which crates to use, which ones fit together, and which defaults to choose. For that, we're working on battery packs, a way to package up this tacit knowledge into a tangible tool.

Source: https://github.com/nikomatsakis/rcn-july-2026
-->

---
layout: default
class: project-slide battery-pack-details-slide
section: battery
---

<BatteryPackDetails />

<!--
Want to build something on embedded but have no idea where to start? `cargo bp add embedded`.

We have a bigger mission here as well; a battery pack codifies what crates a group of practitioners see as the ones worth rallying around. As these recommendations emerge we can try to support this key set of primitives.

Sources:
- https://github.com/nikomatsakis/rcn-july-2026
- https://github.com/battery-pack-rs/battery-pack
-->

---
layout: default
class: closing-qr-slide
section: battery
footer: false
---

<ClosingQr />

<!--
You can find these projects and more at rust-at-aws.github.io.
come find us at our booth!
-->
