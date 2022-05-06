# Developer Advocacy

## 1 - How do you identify learning opportunities for contributing developers in an organization?

An opportunity in the context of an organization is something that moves the organization, division, team, or individual closer towards a stated goal, thus the first step is to understand the goal.

Learning opportunities for organizational goals are often self-generated when those goals, and the reasons behind them, are communicated clearly. After an initial broad communication a small group of passionate individuals usually work their way through their managers, skips, and other channels to voice their opinions, share their thoughts, express concern and/or desire to be part of the effort. Aligning with that group is one key part of pushing broad changes, otherwise they'll be blockers if they're not onboard.

Following the initial communication an assessment is needed to continually gauge each team's expertise and gaps, what training is required, and how each particular team learns best. Creating a light-weight assessment process helps with continual measuring and monitoring of the learning effort.

For individuals looking to grow themselves personally it's often best to have their manager look for opportunities that best suit the developers career goals and learning style. If an IC is looking to learn skills outside their team's daily rituals they can work with an internal PM team that handles career growth or to find other teams looking to host a dev for a few sprints to get exposure.

## 2 - What makes a developer advocate successful? How do you measure that?

The developer advocate role in this context is new to me but when I picture my ideal advocate it's [Scott Hanselman](https://www.hanselman.com/). He's always learning new technologies, interviewing people across the industry, brings true excitement to the technologies he showcases, and he's always, always coding and learning. Developers trust him to the point of trying things they might normally have resisted. 

A developer advocate lives, breaths, loves development and they bring that to the people they interact with. People want to try new things because the advocate is honest, direct, and comes off as a nerd excited about something rather than slick and slippery marketing or sales hype.

The first measure of success is if people want to listen to the advocate, otherwise they're just another thing to be dealt with in an already stressful and overworked day. I read Hanselman's blogs and listen to his podcasts when I want to have fun and I setup my RSS reader to always ping me when he has something new.

There is a whole paragraph I could write about aligning to goals, measuring KPIs, setting up clear processes, keeping things light-weight, continual measuring, dashboards, blah, blah, etc. but those are the obvious, easy, and, well, boring. Advocates bring passion, deep knowledge, and they don't feel like they're there to sell you something.

## 3 - Describe the most effective techniques you’ve discovered, learned or used for changing ingrained behaviors and practices in an engineering organization. What made it/them effective

1. Identify key, respected leaders and change their mind first

   Often it's a few, key individuals that prevent an organization's behaviors from changing. I've seen that person and I've been that person, where I was respected enough that it didn't matter what our directors, VPs, CTOs, etc. where saying because a large chunk of people looked to me as someone that was honest and wouldn't sugarcoat it. Sometimes I was right, sometimes I was wrong, but finding those people and working with them in small groups with full transparency makes a huge difference. Often they become the biggest champion for chance once swayed to the dark side.

2. Explain the reason for the change and put the constraints out there for everyone

   No one likes being told to do something, "just because". Present the reason behind the change, any constraints that informed the change (_"only MIT and Apache open-source are allowed"_, _"no vendors that contribute to hate groups"_, _"needs to support Python 3.x, Go, and Ruby"_), and why the other options were rejected.

   This makes the choice seem less arbitrary, expands their view beyond just themselves, and feels inclusive. It can also sometimes lead to hidden SMEs coming forward to help offer experienced views.

3. Make it better, not just different

   Anyone that's been around awhile has experienced massive changes that ended up only being different, not better, and thus a huge waste of time. Show the value.

4. Remove the issue via automation

   For DECADES people fought over tabs vs. spaces, indentation level, naming conventions, etc. but that all ended when people started integrating linters into their PR CI process. Code is automatically linted to conform to the organization's coding standards so for the hold outs that really can't get past using two spaces instead of four... well, let them have at it, it'll get normalized on commit.

5. Blame the robots via automated quality gates

   Similar to above but throw a pipeline decorator into your CI/CD build that blocks code moving from the dev environment unless it has greater than 90% code coverage, or if it has any high priority bugs reported by your SAST/DAST tooling, or whatever else, and remove any ability to bypass or get an exception.

   No favorites, no exceptions, applied globally to the organization.

## 4 - An engineering manager asks you to take on a mentoring relationship with an underperforming developer on her team. How would you respond, and what actions would you take?

"Underperforming" often has a connotation of not meeting goals, poor time management skills, friction-filled interpersonal interactions, less than honest responses, and is often the precursor to a performance improvement plan, which sadly most often leads to managing out.

My first reaction is that I'm the wrong person for them to talk to about their report so I'd spend time understanding what they mean by underperforming and why they feel I'm the best person to help address the issue. Managing the performance of each and every individual on their team is the most important aspect of a manager's job, I'd support them as much from an advocate role as possible but since performance relates to compensation and salary I'd get very crisp around expectations.

Assuming the issues aren't interpersonal, which should be handled by the management chain and HR, but technical, I'd suggest they pair the individual with senior developers inside their team. Team members have the most context and are already using the skills needed by everyone so pairing is usually my first step.

If it's broader technical skills I'd ask the manager to provide the expected skill set level for their team and ask that they incorporate learning cycles into their sprints. Allow the individual a sprint or two to learn how they learn best, create a POC, and present their projects and findings so they're accountable.

## 5 - What is your perspective on technical debt? How would you coach developers and teams on managing debt based on that perspective?

"Technical debt" is a natural part of the care and feeding of all software and must be built into any healthy development life-cycle. Software is **never** done, it must always be maintained and kept current, especially these days with security and privacy concerns. It is not at odds with feature work, it supports it.

### Balancing engineering excellence with product work

1. Know you'll never "catch up"
1. Get Product on board with **why** it's so important so they become a champion for continual improvement instead of feeling as if they're always having to trade one for the other
1. Run regular retros and reviews to get feedback from the developers actually touching the code to understand what's causing them the most pain, thus causing them to be unproductive
1. Communicate changes before, during, and after
1. Make no large-scale changes without a way to test the changes
1. Asses the impact
1. Be honest about the shiny vs. the needed

## 6 - A development organization has 5 teams, each with their own codebase, tech stack, and set of processes for how they conduct their work. What are some benefits and challenges inherent in that model? How would you approach creating alignment across those teams?

Disparate tech stacks and team rituals can foster innovation, experimentation, provide a broader hiring pool, increases team morale, and allows for greater team bonding when allowed to help craft their own daily rituals.

That freedom can create challenges for organizations looking to move people rapidly between projects since each team requires a unique onboarding experience. It makes spinning up new teams more difficult without an off-the-shelf set of practices, rituals, guidelines and expectations. Some teams prefer having a stock "starter kit" vs. wasting time re-inventing the wheel.

It can impact big picture planning if different teams use different estimation methods, it makes compliance more complicated and puts more burden on any shared services teams that now must support dozens of tools and approaches instead of a few.

For alignment I'd work with the directors to establish an interface model, where we define what each team needs to provide but not how or with tools they must use.

For example...

```csharp
# Actions and responsibilities required from each team, without defining the who or how
#
# - can be a PM, PO, DM or rotating IC, up to the team
# - each team has a working agreement that outlines their implementation
#
interface ITeam
{
    # daily rituals
    string ProvideStatus();
    void TriageBugs();
    void RunStandUp();

    # reporting/metrics

    # each app must report it's code coverage, doesn't matter how
    # it's generated but it must upload it to a unified location (SonarQube, etc.)
    float ReportCodeCoverage(string applicationName);

    # doesn't matter which test runner or language they use, but
    # all applications must have unit tests
    bool RunUnitTests();

    # doesn't matter if ks.io or JMeter or whatever, but all
    # teams must have performance tests and they must
    # be uploaded to a defined data store for org-wide reporting
    bool RunPerformanceTests();
}
```

These contracts can then be used to put quality checks in place, for example _"no services/apps/code gets to production without 90% code coverage"_ or _"no code allowed if there are any SonarQube (or whatever SAST/DAST tools) security issues"_, etc.

