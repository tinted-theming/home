# Contributing

Welcome to Tinted Theming, a community-driven project focused on
creating and sharing themes. Our mission is to build a diverse
collection of themes that can be easily adopted and customized. Whether
you're looking to contribute your existing theme, join as a maintainer,
help out with design, take part in discussions or report bugs, we're
excited to have you on board.

## Joining Tinted Theming

Contributors can join the Tinted Theming Github organization in the
following ways:

1. Join an existing repository as one of the maintainers
1. Transfer your repository into the Tinted Theming organization and
   become a maintainer of that repository

## Repository Transfer Process

### Acceptance criteria

Before transferring your repository, please ensure it meets the
following criteria:

- Follows our [Code of Conduct] and contribution guidelines
- Aligns with Tinted Theming's thematic and aesthetic standards
- Includes at least basic documentation on theme usage

### Agreement

When a repository is transferred to Tinted Theming, it then belongs to
the Tinted Theming Github organization and community. The previous owner
changes from being the owner of the repository to a maintainer of the
repository. It is not mandatory to be a maintainer after transferring,
but we recommend it.

Due to how Github deals with redirects, we recommend not re-creating a
Github repository with the same URL after transferring since it will
break the redirect from the old repository URL to the newly transferred
repository.

### Process

The process for transferring a repository into Tinted Theming is as
follows:

1. [Contact us] about transferring the repository
1. If your repository passes the [acceptance criteria] you will receive
   an invite to join the organization
1. Accept the invite
1. Go to the Settings page of the repository you want to transfer and
   scroll to the bottom. You will see a "Danger Zone" section which
   contains the option to "Transfer ownership".
1. Click "Transfer ownership" and select Tinted Theming as the
   organization you want to transfer to

The steps on your side are now complete. Next steps an admin will take
will be:

1. Add you to a relevant Github team
1. Add the team as the maintainer of the newly transferred repository
1. If not already done, the primary branch will be set to `main`
1. If the repository is a theme template repository, a PR will be
   created which sets up [@tinted-theming-bot] to run [builder] on on
   the repository once a week to make sure it is up to date with the
   [latest schemes]

### How to get in contact?

File an issue in this repository, stating you would like to transfer a
repository.

## Maintainer Obligations

When you choose to become a maintainer you're taking on a role that's
vital to the health and growth of our community. As a maintainer, your
obligations include but are not limited to the following:

- **Code Quality and Review**: Maintain the quality of the repository's
  codebase, review and merge pull requests, and ensure contributions meet
  the project's standards and guidelines.
- **Community Engagement**: Participate in discussions, answer
  questions, and help resolve issues within your repository. A responsive
  maintainer fosters a positive community and encourages more
  contributions.
- **Documentation**: Maintain and update the documentation for your
  themes to ensure that users and contributors have clear guidelines on
  how to use, customize, and contribute to the themes.
- **Continuous Improvement**: Where it makes sense, regularly update the
  repository with improvements, bug fixes, and enhancements to keep the
  themes relevant and functional across different platforms.
- **Inclusivity**: Uphold the principles of our [Code of Conduct] by
  promoting an inclusive and welcoming environment for all contributors
  and community members.

Becoming a maintainer is a commitment to supporting the Tinted Theming
community and helping it thrive. While it is a voluntary role, we look
for individuals who are passionate about theming and willing to invest
their time in nurturing their repositories and the community around
them.

To make sure we keep things in a good state, it's important for people
to understand and accept the above before becoming a maintainer.

Maintainers who do not adhere to the obligations may be removed from the
maintainer team. This does not mean they cannot reapply as maintainers
in future.

## Support for Maintainers

We understand that taking on the role of a maintainer can be a
significant commitment. Tinted Theming provides support and resources to
maintainers, including:

- **Community Support**: Our maintainer community is a space for sharing
  best practices, seeking advice and collaborating on projects. Our
  [Matrix] channel is a great place for less formal chats.
- **Recognition**: Maintainers are recognized for their contributions
  and dedication.

We encourage anyone considering becoming a maintainer to reach out with
questions or for more information on what the role entails. Together, we
can continue to build a vibrant and diverse theming community.

[@tinted-theming-bot]: https://github.com/tinted-theming-bot
[builder]: https://github.com/tinted-theming/base16-builder-go
[latest schemes]: https://github.com/tinted-theming/schemes
[create a Github issue]: https://github.com/tinted-theming/home/issues
[Matrix]: https://matrix.to/#/#tinted-theming:matrix.org
[Code of Conduct]: ./CODE_OF_CONDUCT.md
[Contact us]: #how-to-get-in-contact
[acceptance criteria]: #acceptance-criteria
