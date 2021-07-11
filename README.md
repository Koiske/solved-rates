# Plugin: `discourse-solved-rates`

Calculating the percentage of topics in a given time span and target category that have a marked solution.

---

## Features

- Adds an admin widget on the plugin page at `%BASEURL%/admin/plugins/discourse-solved-rates` that allows an admin user to find the percentage of topics (between two dates and in a given category) that have a post marked as the solution.

  <img src=docs/discourse-solved-rates.png>

  - This hooks into the functionality provided by the [discourse-solved](https://github.com/discourse/discourse-solved) plugin, which allows users and staff to mark a post that solves a topic.

---

## Impact

### Community

None, not visible to non-admin users.

### Internal

Enables tracking the percentage of solved posts in certain categories, as a metric for community health or engineering performance.

### Resources

Every time the widget is used, a database query is submitted that needs to scan over all the topics in the given category. This is a medium-sized workload that might take a minute to complete for categories with a really high amount of topics.

When the widget is not in use, there is no performance impact.

Whenever an operation is performed through this widget, it scans through the database of topics for that category, and for each topic checks whether it falls within the given date range. It then checks whether each topic that matches those criteria has a marked solution.

### Maintenance

No manual maintenance needed.

---

## Technical Scope

Whenever an operation is performed through this widget, it scans through the database of topics for that category, and for each topic checks whether it falls within the given date range. It then checks whether each topic that matches those criteria has a marked solution.
