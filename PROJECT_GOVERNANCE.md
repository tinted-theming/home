# Tinted Theming Project Governance

Welcome to the Tinted Theming project! This document outlines the
governance structure and procedures for maintaining and contributing to
this theming driven community.

## 1. Project Governance and Final Decision Authority

The Tinted Theming project is currently governed by three admins:

- [@balek], who has been actively involved in the community since the
  original base16 theming project.
- [@JamyGolden], who has been actively involved in the formation of
  base16-project and tinted-theming.
- [@FredHappyface], who recently joined the administration team.

**Final Say:** The three admins collectively have the final say on all
matters related to the overall direction, policies, and major decisions
concerning the project. This ensures that the project remains true to
its core values and goals while also allowing for flexibility and
community input.

Project-wide decisions are typically made through consensus among the
admins. In cases where consensus cannot be reached, a majority vote
among the admins will determine the final decision.

### Unresponsive Maintainers

If a template maintainer does not respond to an issue or pull request
(PR) within a **reasonable timeframe** (typically **3 weeks**), the
admins may step in to make a decision on behalf of the maintainer. This
ensures that the project continues to move forward and that
contributions are not stalled unnecessarily.

The process in such cases will be as follows:

1. **Initial Attempt:** Contributors should first try to contact the
   maintainer via the issue or PR thread.
2. **Escalation:** If there is no response after **3 weeks**, the issue
   or PR can be escalated by tagging the admins in a comment;
   @tinted-theming/admins to tag all admins.
3. **Admin Decision:** Admins will review the situation and may:
   - Reach out to the maintainer through other means.
   - Make a decision on the issue or PR if the maintainer remains
     unresponsive.
   - Appoint a temporary or new maintainer if the original maintainer is
     no longer active.

### Unresponsive Admins

In cases where the admins are unresponsive (e.g., no response for **4
weeks** on an escalated issue or PR), the community can take the
following steps:

1. **Community Discussion:** Open a discussion issue or use the
   project's designated communication channel to gather input from other
   contributors and maintainers.
2. **Community Consensus:** If a clear consensus is reached within the
   community (with input from other maintainers), the decision can be
   acted upon by those involved in the discussion.
3. **Request Admin Intervention:** If possible, attempt to contact
   admins through other channels (email, social media, etc.) to notify
   them of the situation.
4. **Temporary Action:** In the absence of admin response, maintainers
   or active contributors may make temporary decisions, such as merging
   a critical PR, until the admins return.

**Note**: If an admin remains unresponsive, the other admins will
continue to carry out their responsibilities and may make decisions on
behalf of the project as necessary. If all admins become unresponsive,
the community should follow the steps outlined above.

**Note**: If maintainers or admins expect to be unavailable for an
extended period, they are encouraged to notify the community in advance,
if possible, to arrange for temporary coverage or decision-making
processes.

### Succession Planning

To prevent prolonged unresponsiveness, it is advisable to periodically
review the activity of admins and maintainers. If an admin becomes
permanently inactive, the remaining admins may appoint a replacement
from active community members. Similarly, inactive maintainers may be
replaced or supplemented by other contributors with a track record of
involvement in the project.

## 2. Template-Specific Governance

Each project within Tinted Theming is managed by a dedicated maintainer
or maintainers. These maintainers are responsible for overseeing the
development, updates, and quality of their respective templates.

**Final Say on Templates:** Maintainers generally have the final say
regarding their specific templates, as they possess the most intimate
knowledge and expertise concerning their design and functionality.
However, admins reserve the right to intervene if a template decision:

- Significantly affects the broader project or community.
- Conflicts with the project's core principles or guidelines.
- Introduces potential security or usability concerns.

In such cases, admins may discuss the issue with the template maintainer
to reach a resolution, and if necessary, admins may have the final say.

## 3. Acceptance Criteria for Pull Requests (PRs)

To ensure the continued quality and consistency of the Tinted Theming
project, all contributions are reviewed against the following acceptance
criteria:

### General PR Criteria:
- **Alignment with Project Goals:** The PR should align with the overall
  goals and philosophy of the Tinted Theming organization.
- **Code Quality:** The code should be clean, well-documented, and
  follow the project's coding standards.
- **No Breaking Changes:** PRs should not introduce breaking changes
  unless absolutely necessary. If a breaking change is required, it must
  be well-documented, and a clear migration path should be provided.
- **Community Feedback:** PRs should consider feedback from the
  community where appropriate. If significant concerns are raised by the
  community, they should be addressed before the PR is merged.

### Template-Specific PR Criteria:
- **Consistency:** The PR should maintain the stylistic and functional
  consistency of the template.
- **Testing:** PRs should include appropriate testing to ensure the
  template functions as expected across different environments and use
  cases.
- **Backward Compatibility:** As much as possible, changes should be
  backward compatible with previous versions of the template.

### Review Process:
1. **Initial Review:** The template maintainer or designated reviewers
   will conduct an initial review of the PR.
2. **Feedback Loop:** If changes or improvements are required, the
   contributor will receive feedback and have the opportunity to address
   it.
3. **Final Approval:** Once the PR meets all criteria and any feedback
   has been addressed, the maintainer or admins will give final approval
   for merging.

For larger changes or additions, maintainers or contributors are
encouraged to open a discussion issue before submitting a PR to gauge
interest and gather early feedback.

For more detailed instructions on how to contribute, please refer to our
[CONTRIBUTING.md] file.

---

We hope this document provides clarity on the governance and
contribution processes within the Tinted Theming organization. Thank you
for your involvement and contributions!

For any further questions, please feel free to reach out to the admins
[@balek], [@JamyGolden] and [@FredHappyface] on Github or on [Matrix
Chat].

[@balek]: https://github.com/balek
[@JamyGolden]: https://github.com/JamyGolden
[@FredHappyface]: https://github.com/FredHappyface
[CONTRIBUTING.md]: ./CONTRIBUTING.md
[Matrix Chat]: https://matrix.to/#/#tinted-theming:matrix.org
