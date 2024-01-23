# $name

$name aims to serve as a public good, providing decentralized and censorship-resistant services for content publishing and communication.
It operates on the public compute infrastructure powered by the [Internet Computer](https://internetcomputer.org).

## Key Points

-   $name combines features of forums and blogs.
-   $name is tokenized and is owned and governed by its token holders.
-   $name is completely ad-free and generates revenue.
-   $name uses its revenue to reward content producers, token holders (pro-rata) and to cover storage and compute costs.

## General features

### Tokens

There are different tokens running the plateform with their own usecase:

-   **Credits** are used to interact with others
-   **$ICP** are used to mint credits
-   **$name** are used to vote for proposals and weight the revenue distribution.
-   **Rewards** are used to weight the revenue distribution.

Here is a little scheme to understand how they are linked:

**$ICP** → **Credits** → _Interaction_ → **Rewards** → _Revenue distribution_

**$name** → \*Revenue distribution

_Revenue distribution_ → **Credits** _or_ **$ICP** _or/and_ **$name**

### Stalwarts

Stalwarts represent the union of top `$stalwart_percentage%` of users with the highest $$token_symbol  balance, active during the last  `$min_stalwart_activity_weeks`consecutive weeks and possessing accounts older than`$min_stalwart_account_age_weeks` weeks.

They are considered trusted community members, authorized to carry out moderating actions and propose upgrades.

### Realms

Realms are sub-communities centered around specific topics. Each realm can establish its own terms and conditions including:

-   a minimal **$name balance**. User without the required amount of $name are not allowed to post on the realm.
-   a minimal **account age** (in days). User with early accounts are not allowed to post on the realm.
-   a minimal **number of followers**. User without enough followers are not allowed to post on the realm.
-   eviction penalty. If a user does not respect the behaviour policy set by the realm controllers. They can evict the post with a credit penalty.

Upon joining a realm, users implicitly agree to its terms and conditions.

Currently, `$realm_revenue_percentage%` of revenue generated inside the realm is shared with its controllers.

## Content and Behavior Policy

Decentralization does not equate to lawlessness!
Content and behavior permitted on $name aligns with community-approved moderation guidelines.
Content and behavior not permitted on $name falls into one of the following categories:

-   Content and behavior that jeopardize $name as a public service (e.g., those illegal in many jurisdictions).
-   Content or behavior detrimental to the community, sustainability, or decentralization of $name.
-   Content created with malicious intent, such as gaming the $name system.
-   Content and behavior that violate realm-specific rules.

This policy is intentionally broad and necessitates social consensus among stalwarts.

**Posts contravening this policy are subject to moderation.**

## Moderation

Moderation on $name is decentralized; anyone can initiate it, and stalwarts can execute it.
Whenever a post or user is reported, all stalwarts receive notifications and are expected to validate or dismiss the report.
Once `$report_confirmation_percentage%` of stalwarts concur on the report's validity, it is closed.
For confirmed reports:

-   The violating user loses `$reporting_penalty_post` (post report) or `$reporting_penalty_misbehaviour` (user report) rewards, along with an equivalent amount of credits.
-   The reporter receives half of this penalty as rewards.

If stalwarts dismiss the report, the reporter loses half the penalty as credits and rewards.
In both cases, participating stalwarts share rewards from the penalty fee, capped at `$stalwart_moderation_reward`.

## Governance

$name is governed via proposals.
There are proposals for upgrading the main smart contract, for minting new tokens for funding & rewards and for transfering $ICP out of the treasury for off-chains activities of the DAO.

A proposal succeeds if `$proposal_approval_threshold%` of users approve it or fails if `(100 - $proposal_approval_threshold)%` of users reject it.
Only tokens of registered users active within `$voting_power_activity_weeks` weeks count as participating votes.
To prevent low-quality proposals, a proposal rejected with a rejected/adopted ratio under `$proposal_controversy_threashold%` incurs a loss of `$proposal_rejection_penalty` rewards and credits for the proposer.

The total voting power of all registered users required to adopt or reject a proposal decreases daily by `1%` while the proposal remains open.
This is achieved by multiplying the total available voting power by a factor `d%`, where `d` is the number of days the proposal remains open.
This ensures any proposal eventually passes within `100` days.

For any pending proposal the following holds until it gets adopted, rejected or cancelled:

-   the $$token_symbol tokens of voters who voted on that proposal are locked and cannot be transferred;
-   the rewards and the token minting are deferred for everyone.

## Tokenomics

$name has a maximal supply of `$maximum_supply` tokens.

### Supply Increase

New tokens can only be mined by users or minted via minting proposals.
Once the maximal supply is reached, both the weekly minting and minting proposal will be suspended.

### Supply Decrease

When a `$$token_symbol` transfer transaction gets executed, the fee of `$fee` gets burned. The amount of credits burned for platform fees is displayed in `WEEK'S REVENUE` value.
Once the maximal supply is reached, the minting and minting proposal will resume after enough fees are burned via transfer transactions.

This will make the supply to keep an equilibrium around the maximal supply.

## Usage Costs and Rewards in Interactions

Each interaction with other users on $name consumes credits.
All payments are directed to [$name's Treasury](https://dashboard.internetcomputer.org/account/dee15d98a70029163c79ace6ec9cf33b21917355f1766f44f87b4cb9f4d3b393) which holds the revenue.
In each interaction, there is an emitter and a receiver. The cost to emit is listed below in the `credits` column. The receiver will then get (or lose _cf Reacting with 👎_) the amount of rewards in the `Rewards` column.

| Function              |       Credits 🔥 |            Rewards | Comments                                     |
| :-------------------- | ---------------: | -----------------: | :------------------------------------------- |
| New post              |     `$post_cost` |                    |                                              |
| New comment           |     `$post_cost` | `$response_reward` |                                              |
| Add Hashtags          |  `T * $tag_cost` |                    | For `T` unique hashtags in a post or comment |
| Add On-chain pictures | `B * $blob_cost` |                    | For `B` pictures in a post or comment        |
| Add Poll              |     `$poll_cost` |                    | For adding a poll to a post or comment       |
| Reacting with ❤️      |              `2` |                `1` | Burns `$reaction_fee` credits                |
| Reacting with 🔥, 😆  |              `6` |                `5` | Burns `$reaction_fee` credits                |
| Reacting with ⭐️     |             `11` |               `10` | Burns `$reaction_fee` credits                |
| Reacting with 👎      |              `3` |               `-3` | Burns `3` credits of post's author           |
| New realm creation    |    `$realm_cost` |                    | Burns `$realm_cost` credits                  |

Notes:

1. Inactive users' credits decrease by `$inactivity_penalty` per week after `$inactivity_duration_weeks` weeks of inactivity.
2. Users with negative rewards balance don't participate in reward distributions or minting.
3. To curb the inorganic behaviour, $name automatically charges excess fees for all posts above `$max_posts_per_day`  per rolling 24h interval and for all comments above  `$max_comments_per_hour` per hour.
The fee is computed by multiplying `$excess_penalty` with the number of excessive items. If the excessive items contain images, the computed excess fee is additionally charged per image.

The revenue distibution will be explained later on.

## Revenue Distribution

Every Friday, a weekly distribution occurs in different ways.

### Rewards distribution

Earned rewards points are converted to $ICP at the ratio `$credits_per_xdr`rewards /`$xdr_in_usd` USD. However, if the users’ credit balance is low, he will receive credits instead of $ICP to help with normie onboarding.

### $name distribution

Users owning tokens and being active within the last `2` weeks receive a share of **$name's revenue** proportionate to their token holdings. The amount of **$name's revenue** is displayed on the dashboard under `REVENUE PAID` value.

All users who earn rewards become eligible for receiving newly minted `$token_symbol` tokens. The amount of minted tokens is computed weekly according to the following algorithm:

1. For every user (U) who rewarded others, $name will mint new tokens limited by the user's  `$token_symbol`balance divided by the minting ratio`R` (see below).
2. The newly minted tokens will be assigned to rewarded users (by U) weighted by their share of received rewards and an additional factor `F` which depends on receiver's `$$token_symbol` balance:

| Receiver's $$token_symbol balance | `F`    |
| --------------------------------- | ------ |
| Below `100`                       | `1.2`  |
| Below `250`                       | `1.15` |
| Below `500`                       | `1.1`  |
| Above `500`                       | `1`    |

The minting ratio `R` is algorithmically computed by $name:

-   It starts at `1:1` and remains at this level until `10%` of supply is minted.
-   Then the ratio decreases to `2:1` for the next `10%`, further decreasing to `4:1`, and so on.

Hence, the last `10%` of supply will be minted at a ratio of `512:1`.

## Team Tokens

`20%` of tokens are allocated to the first two users forming an informal bootstrapping team before the tokenization:

-   `18%` to @X (founder and the only software developer),
-   `2%` to @mechaquan (growth & marketing).

Tokens are minted weekly, with each user receiving an amount equal to `1%` of the current supply if and only if one of the following conditions are met:

-   Their individual share is below `14%` of minted supply.
-   `2/3` of the total supply has been minted.

Vesting tokens:

-   @mechaquan: `$vesting_tokens_m`
-   @X: `$vesting_tokens_x`

## Technical aspects

### Autonomy

$name is designed for full autonomy, guided by decentralization.
It autonomously creates new storage canisters when space runs out.
$name tops up canisters with low credits using ICP from the Treasury.
The [dashboard](/#/dashboard) provides information on system status and past events.

### The $name Network Neuron

$name DAO votes on NNS proposals with neuron [$neuron_id](http://dashboard.internetcomputer.org/neuron/$neuron_id) and doesn't follow anyone.

### Neuron Decentralization

The neuron is only controlled by $name's canister as the assigned neuron's controller lacks a known secret key.
The $name canister votes via the hot-key mechanism.
$name canister's `get_neuron_info` method confirms this:

    dfx canister --network ic call $canister_id get_neuron_info

### Voting

Proposals categorized as "Governance", "Network Economics", "Replica Version Management," and "SNS & Community Fund" display as posts with polls.
$name canister votes on these proposals after 3 days, weighted by voters' token balances.

Other proposals are automatically rejected.
$name DAO commits to:

1. Attract voters to other topics over time.
2. Find followees or vote themselves if automated rejection harms #IC.

### Bots

$name users can become bots by adding principal IDs in account settings.
These IDs (canisters or self-authenticating) can call $name's `add_post` method in Candid format as follows:

    "add_post": (text, vec record { text; blob }, opt nat64, opt text) -> (variant { Ok: nat64; Err: text });

Arguments:

-   `text`: body text.
-   `vec record {text; blob}`: vector of attached pictures, each tuple containing a blob ID and the blob itself. Tuple requirements:
    -   ID length < `9` characters.
    -   Blob < `$max_blob_size_bytes` bytes.
    -   Pictures referenced from the post by URL `/blob/<id>`.
-   `opt nat64`: parent post ID.
-   `opt text`: realm name.

Note: #IC doesn't support messages > `2Mb`.
The result of `add_post` contains the new post's ID or an error message.

### Code and Bug Bounty

$name's [code](https://github.com/TaggrNetwork/taggr) is open source, under GPL license.


$name's DAO has a bug bounty program with classifications and rewards in `$token_symbol`.

| SEV | DESCRIPTION                                                                                                                           | BOUNTY |
| :-: | ------------------------------------------------------------------------------------------------------------------------------------- | -----: |
|  0  | Bugs enabling unsanctioned state mutations affecting assets like credits, rewards, tokens, Treasury, or critically endangering $name. | `1000` |
|  1  | Bugs enabling unsanctioned state mutations affecting data, with moderate impact on decentralization or autonomy.                      |  `400` |
|  2  | Bugs enabling unsanctioned state mutations without substantial impact on $name.                                                       |  `100` |

Report bugs to stalwarts immediately if they fall under any of these categories.
