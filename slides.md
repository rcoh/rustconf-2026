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
Hello! I'm Russell, I work on Rust at Amazon. Today I want to share 4 new OSS tools that Rust developers are Amazon that you can use immediately.
-->

---
layout: default
class: about-slide
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
When folks at Amazon started using Rust, Rust still looked like this. If you were not around in those days, you might be amused by some of the syntax.

[click] The tildes — `~[~str]` — were the old sigils for owned and boxed pointers.

[click] The `@int` was a managed, garbage-collected pointer.

[click] And `proc()` was a built-in one-shot closure for spawning tasks.

That was back in 2014. By 2016 a few intrepid folks got a real build system working. Rust's share in the Amazon developer population has been growing ever since.
-->

---
layout: default
class: timeline-slide
---

<TimelineSlide />

<!--
2014 was the first use of Rust at Amazon. By 2016 a few intrepid folks had a real build system working.

And then, recently, something changed: AI got good at Rust.
-->

---
layout: image
image: /images/langtrends/final-open-tr-light.svg
class: growth-chart-slide
backgroundSize: contain
---

<!--
Rust's share of Amazon developers is now growing faster than any other major language. 

There has never been a single day in the last 8 years when year-of-year portion of Amazon builders using Rust has gone down.
-->

---
layout: image
image: /images/fleet-scale-meme.png
class: fleet-meme-slide
backgroundSize: cover
---

<!--
And obviously part of this growth is AI. But another part of it is that at Amazon scale, Rust's promises of performance, safety, and productivity just _work_.
-->

---
layout: statement
class: so-what-slide
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
---

# Four things you can use now.

<div class="project-index">
  <div><span>01</span><strong>metrique</strong><small>production metrics</small></div>
  <div><span>02</span><strong>dial9</strong><small>runtime traces</small></div>
  <div><span>03</span><strong>Shuttle + Turmoil</strong><small>deterministic failures</small></div>
  <div><span>04</span><strong>Hydro</strong><small>distributed programs</small></div>
</div>

<!--
I'll start with metrique
-->

---
layout: default
class: project-slide metrique-slide
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
Amazon does metrics a little bit differently from a lot of other companies. We're heavily focused on "wide event" (aka unit-of-work) metrics. This is where the metrics that you see on a graph don't come from a counter in your code, instead they come from an _event_ your code emits that turns into a counter.

In both cases, you have a metric in a dashboard somewhere. But if your metrics from wide events, you have receipts to connect the graph to an actual event in your system.
-->

---
layout: default
class: project-slide code-slide
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
metrique makes those events plain structs with helpful primitive to handle things like timestamps and units. It's agnostic to the actual output format.

[click] Inside of Amazon, unsurprisingly, we have a metrique backend for our own gnarly metric format. But the same struct also emits plain JSON, EMF, otel, a pretty format just for local debugging (and even dial9).
-->

---
layout: default
class: project-slide dial9-slide
---

<div class="project-number">02</div>

<div class="dial9-copy">
  <h1>dial9</h1>
  <p>A flight recorder for Rust.</p>
  <a href="https://dial9-rs.github.io/blog/dial9-a-flight-recorder-for-rust/">dial9-rs.github.io</a>
</div>

<!--
So a quick story; earlier this year, I got pulled into a performance investigation for a team that was onboarding to Rust. To figure out their performance problem, we really needed to pull lots of events from Tokio, in production. Anyway, long story short, turns out, if you run Tokio and also 16k Java threads on the same host it doesn’t work super well.

But along the path of solving this, we build dial9 which lets you capture lots of data on a production host and then upload to S3 so you can analyze it later.

It started as a tool just for Tokio; and tokio produces a ton of events. We ended up with something pretty high performance.
-->

---
layout: default
class: project-slide dial9-encode-slide
---

<div class="project-eyebrow">02 &middot; dial9</div>

<Dial9Encode />

<!--
dial9 was originally built to record every single event coming off of Tokio; for a large production application this is routinely in the 100k to 1M/s range across many cores.

So take one event that represents a "poll start".

[click] If you wanted to encode that with tracing + json_subscriber, it takes almost a microsecond. Which is not a lot, but at this event rate it quickly becomes expensive.

[click] The same event in dial9's binary format takes about 22 nanoseconds.

[click] That's roughly 48x cheaper to emit — which is what lets you record every single poll on a production host. (OTLP protobuf sits in the middle, around 345ns.)
-->

---
layout: default
class: project-slide dial9-sources-slide
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
-->

---
layout: image
image: /images/dial9-shot-1.png
class: shot-slide
backgroundSize: contain
---

<!--
And once you have all this data in one place, you can do some pretty cool stuff. For example, you can look at the slowest instance of a particular request, then jump
-->

---
layout: image
image: /images/dial9-shot-2.png
class: shot-slide
backgroundSize: contain
---

<!--
directly the the individual poll, and see why it was slow. In this case, dial9 shows that the thread was descheduled by the kernel trying to acquire a lock.
-->

---
layout: default
class: project-slide testing-slide
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

Shuttle and Turmoil attack the same problem at different layers.

Shuttle explores different schedules in concurrent Rust code. Turmoil runs multiple hosts in one deterministic simulation and lets the test control the network.

dial9 uses shuttle to validate our cross threaded event bus. S3 uses shuttle to validate that its metadata storage works as expected.

I went looking for an example bug caught with shuttle that I could share on a conference talk slide; but the bugs shuttle finds are very complicated and that is kind of the point. Shuttle finds bugs that are only reachable in complex scenarios between interacting threads. If this describes your code, its worth taking a look.
-->

---
layout: default
class: project-slide hydro-slide
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
Hydro asks the more ambitious question: can the programming model make some distributed mistakes harder to express at all?

Hydro lets you describe a distributed system as one Rust program, then compiles that program into a deployment plan and code for each machine.
-->

---
layout: statement
class: closing-slide
---

<p>The next phase is not proving that Rust can run at scale.</p>

# It is making ambitious systems easier to trust.

<div class="closing-projects">metrique &middot; dial9 &middot; Shuttle &middot; Turmoil &middot; Hydro</div>

<!--
In 2020, making Rust work at Amazon meant filling in the basic ecosystem. Today, AI can produce code much faster, but production systems still need evidence.

Metrique gives us evidence from production. dial9 explains runtime behavior. Shuttle and Turmoil turn nondeterminism into repeatable tests. Hydro pushes correctness into the programming model itself.

The next phase is not proving Rust can run at scale. Amazon has been doing that for ten years. It is making ambitious systems easier for many teams to trust.

Thank you.
-->
