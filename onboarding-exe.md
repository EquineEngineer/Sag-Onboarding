# Welcome to SAGittarius!

- [Welcome to SAGittarius!](#welcome-to-sagittarius)
  - [What is SAGittarius?](#what-is-sagittarius)
  - [Dashboards and Data Transformation](#dashboards-and-data-transformation)
    - [What's a Dashboard?](#whats-a-dashboard)
    - [What is Data Transformation?](#what-is-data-transformation)
  - [Grafana as a target](#grafana-as-a-target)
  - [Your role in the project](#your-role-in-the-project)
    - [Training](#training)
    - [Active Development](#active-development)

## What is SAGittarius?

Hi!

If you're reading this, you have received an offer to join the SAGittarius development team and are wondering where to find resources to start your journey as a researcher.

Either that, or you've hacked into my machine. In such case, kudos to you, please don't touch my duck memes collection, it is a very prized and personal possession of mine.

As you might have heard, the SAGittarius project has set for its own goal to develop a low-code platform that generates dashboards from settings files.

If any question you might have is not included in this document, please write to [me](mailto:21imc10066@fh-krems.ac.at).

## Dashboards and Data Transformation

### What's a Dashboard?

Dashboards are visual representations of data that are used to monitor and analyze information about a service or a process.

### What is Data Transformation?

Data transformation is the process of converting data from one format to another. This is done to make the data more suitable for a specific use case.

## Grafana as a target

Grafana is an open-source platform for data visualization, monitoring and analysis. It is used to generate dashboards from data.

We can customise Grafana dashboards by using a JSON-based language called [Grafana Dashboard JSON](https://grafana.com/docs/grafana/latest/reference/dashboard/). Such language is a new target for Sagc and it is still a work in progress.

In order to support Grafana, two more steps are required:
- Developing a python script that takes the resuling JSON file and adapts it to the Grafana Dashboard JSON format.
- Defining which options are available for each widget and coming up with appropriate data structures and defaults.

The source files have a `.ssd` extension and are written in a custom language that is defined by the compiler. The language is still a work in progress and is subject to change.

Each `.ssd` file is comprised of 4 sections:
- `service`: contains the name of the service that will be used to generate the dashboard and related metadata.
- `data`: contains the data that will be used to generate the dashboard.
- `application`: describes the application to be output by the compiler.
- `deployment`: enumerates the deployment targets and environments for the finished application.

What Sagc does, is take the settings file and parse it into multiple Rust structs.
These data structures have a 1:1 mapping with the sections of the settings file and can be loaded into json without losing any information. This is done by using the `serde` crate.
By doing so, json serves as a sort-of intermediate representation (IR) of the settings file.

Then, depending on which kind of application to produce, different adapters (also called compiler backends) are used to generate the final output. Our main target that we're working on right now is `Grafana`.

## Your role in the project

### Training

For the first weeks, there's no expectation you'll be very productive. And that's alright, because neither are the developers working on this since the beginning.

Here follows a list of good resources to learn:

- [Grafana Documentation](https://grafana.com/docs/grafana/latest/)
- [Polars Documentation](https://www.pola.rs)
- [Python Typing Module](https://docs.python.org/3/library/typing.html)


### Active Development

Your main job will be to expand on the Python transpiler functionality and make interfaces for the new Grafana backend. You will be working together with Egor on such task.

You will be expected to:
- Write code that is easy to read and understand.
- Compile accurate documentation when necessary.
- Respect the PR workflow.
- Communicate whenever you're stuck or need help. 
