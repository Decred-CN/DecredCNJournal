# Decred Journal – December 2019

![abstract art](img/journal-201912-384.png)

_Image: Icyhedron by @saender_

Happy New Year! Decred highlights for December:

- The final v1.5 release occurred on Dec 16, thanks to everyone who helped out by testing release candidates.

- The PoS and PoW upgrade thresholds to trigger the headercommitments consensus rule change vote have already been met. The voting period will begin around Jan 16 when the new Rule Change Interval begins.

- Decred Lightning Network is live on mainnet! Check out @jholdstock's network [explorer](https://ln-map.jamieholdstock.com/). So far @matheusd is winning with 11 channels open. Remember: Lightning Network is still considered unstable, experimental, maybe even dangerous! Even experts like Matheus are only playing with a couple of credits.

- Stakeholders approved a $30K budget for funding the ongoing development of TinyDecred, an open source Python toolkit.

## v1.5 Upgrade Notice

v1.5.0 release is out after about 5 weeks of testing and polishing. The new version brings many improvements covered in [October](201910.md#v15-release-candidates) issue. For full release notes and downloads visit the [release page](https://github.com/decred/decred-binaries/releases/tag/v1.5.0) on GitHub. As always, [verify the downloads](https://docs.decred.org/advanced/verifying-binaries/) before installing.

If you're mining and haven't upgraded, it is recommended to upgrade to avoid potentially having a block rejected due to being an old version.

Upgrade and vote progress is shown at [voting.decred.org](https://voting.decred.org/), more details and charts are available at dcrdata's [agendas](https://explorer.dcrdata.org/agendas) page.

Finally, don't forget to set voting preferences for the `headercommitments` agenda in your VSP accounts and solo voting configuration.

## Development

[dcrd](https://github.com/decred/dcrd): Checkpoint logic [simplified](https://github.com/decred/dcrd/pull/2014) to pave the way to support checkpoints based on headers alone. Checkpoints are now also [configurable](https://github.com/decred/dcrd/pull/2013) by the caller. Orphan handling decoupled and [moved](https://github.com/decred/dcrd/pull/2008) from blockchain to block manager. In the bigger picture, these changes will help to decouple the connection code from the download logic, as required for [multi-peer](https://github.com/decred/dcrd/issues/1145) parallel downloading.

Memory usage of conditional execution logic in txscript [optimized](https://github.com/decred/dcrd/pull/2011) by replacing the condition stack with two integers.

Support for bech32 addresses enhanced with convenience functions [added](https://github.com/decred/dcrd/pull/2025) and [ensuring](https://github.com/decred/dcrd/pull/2024) the human-readable part is lowercase to comply with BIP173.

Memory leak [fixed](https://github.com/decred/dcrd/pull/2027) that was especially relevant for setups that involve wallets with a very large number of addresses.

[dcrwallet](https://github.com/decred/dcrwallet): createrawtransaction method [implemented](https://github.com/decred/dcrwallet/pull/1623) directly in dcrwallet so it may be called in SPV syncing mode or when the wallet is not syncing. It was previously only available in RPC syncing mode and required running a dcrd instance.

txsizes package was [exported](https://github.com/decred/dcrwallet/pull/1573) for reuse by dcrdex and dcrdata.

[Decrediton](https://github.com/decred/decrediton): Numerous bugs squashed, including a bug in [Trezor wallet](https://github.com/decred/decrediton/pull/2362) that could be triggered if the Trezor wallet received funds from a non-dcrwallet sender that did not set the Sequence field properly.

[Politeia](https://github.com/decred/politeia): The main focus of Politeia development for December was fixing an issue where [status change](https://github.com/decred/politeia/pull/1073) signature was not saved, and another where [start vote](https://github.com/decred/politeia/pull/1088) signature was only a signature of the proposal token while it should be a signature of the entire Vote structure (which also includes vote params and options). The issues had no impact on users. The fixes are not backwards compatible so they required versioning the metadata. Since versioning of the start vote metadata was required anyway, the second fix also adds changes that will make supporting [RFP proposals](https://github.com/decred/politeia/issues/966) easier.

Backend work to support CMS continues, CMS UI redesign is [in progress](https://github.com/decred/politeiagui/pull/1605).

[dcrpool](https://github.com/decred/dcrpool): Added backend support for processing manual [payment requests](https://github.com/decred/dcrpool/pull/140), which allows to clear any remaining balance before leaving the pool. Extensive [test coverage](https://github.com/decred/dcrpool/pull/141) added for most components.

[dcrlnd](https://github.com/decred/dcrlnd): Map of the Decred LN on mainnet is [live](https://ln-map.jamieholdstock.com/). Note that while LN has been integrated into Decrediton, it should still be considered as in alpha form. If looking to use LN on mainnet, it is recommended to start on testnet, make sure you're comfortable with operations you want to do on mainnet, and not use large amounts.

Port selection [modified](https://github.com/decred/dcrlnd/pull/62) to make integration tests more robust. Docker build [added](https://github.com/decred/dcrlnd/pull/67) to Github actions. Removed [decred prefix](https://github.com/decred/dcrlnd/pull/68). Work continues on [Docker examples](https://github.com/decred/dcrlnd/pull/66) to automate simnet environments with all you need to run a LN cluster.

[dcrdex](https://github.com/decred/dcrdex): New components implemented include [BTC exchange wallet](https://github.com/decred/dcrdex/pull/72), [client orderbook backend](https://github.com/decred/dcrdex/pull/79) and further [integration](https://github.com/decred/dcrdex/pull/85) between the market manager, order router and book routers.

In other changes: [order commitments](https://github.com/decred/dcrdex/pull/83) added to spec, order timestamp resolution changed from seconds to [milliseconds](https://github.com/decred/dcrdex/pull/96), completed switch to [coin ID](https://github.com/decred/dcrdex/pull/91), which allows for supporting more assets in the future.

Remaining tasks for the DEX are:

- on the server: DEX manager that holds all the subsystems together (under review) and a terminal app (in progress)
- on the client: web UI (under review), terminal UI (in draft), DCR wallet (under review), book manager and a persistent database (under review)
- RPC servers for the server and the client

[dcrandroid](https://github.com/decred/dcrandroid): Major [redesign](https://github.com/decred/dcrandroid/pull/401) of the user interface is finally merged after many months of work. This big change also included multi-wallet support (running more than one wallet concurrently). Remaining Java code and files have been converted to Kotlin. On the backend, multi-wallet support was [added](https://github.com/raedahgroup/dcrlibwallet/pull/57) to dcrlibwallet, which uses a modified version of dcrwallet's SPV module to sync all wallets in one process.

Other UI improvements include showing progress bar and estimated time remaining when [rescanning](https://github.com/decred/dcrandroid/pull/414) and the QR code scanner gaining the ability to detect [payment amounts](https://github.com/decred/dcrandroid/pull/411).

Security enhancements: users can now unlock the app with their [fingerprint](https://github.com/decred/dcrandroid/pull/413), address validation was [moved](https://github.com/decred/dcrandroid/pull/421) to security tools.

[dcrios](https://github.com/raedahgroup/dcrios): UI enhancements continue with updated [colors](https://github.com/raedahgroup/dcrios/pull/556) and [improved](https://github.com/raedahgroup/dcrios/pull/555) menu rendering.

Work continues on [multi-wallet](https://github.com/raedahgroup/dcrios/pull/558) support, and revamped UI for [send](https://github.com/raedahgroup/dcrios/pull/557) and [receive](https://github.com/raedahgroup/dcrios/pull/553) views.

[dcrdata](https://github.com/decred/dcrdata): Merged initial CSPP [mix detection](https://github.com/decred/dcrdata/pull/1610), bug fixes and code maintenance.

[tinydecred](https://github.com/decred/tinydecred): Added display of current voting agendas and a menu to set [vote choice](https://github.com/decred/tinydecred/pull/25), automated code formatting with the [Black](https://github.com/decred/tinydecred/pull/27) tool, bug fixes and test improvements.

[docs](https://github.com/decred/dcrdocs): Docs [updated](https://github.com/decred/dcrdocs/pull/1005) for v1.5 release. Warning about scam airdrops [added](https://github.com/decred/dcrdocs/pull/1035). [Forking terms](https://github.com/decred/dcrdocs/pull/1018) added to Glossary.

[decred.org](https://github.com/decred/dcrweb): Minor content updates, dependency upgrades.

Other:

- @degeri [released](https://twitter.com/degeri_crypto/status/1206639882485075968) site compromise notifier called [DownloadHawk](https://github.com/degeri/DownloadHawk), which watches the Decred downloads and raises the alarm if they're tampered with.
- As a [reminder](https://twitter.com/decredproject/status/1208067535532437511), security researchers can earn up to $25K for finding security issues in Decred software. Details at [bounty.decred.org](https://bounty.decred.org/).

Dev activity stats for December: 41 active PRs, 242 master commits, 55K added and 45K deleted lines spread across 15 repositories. Contributions came from 1-5 developers per repository.

## People

Welcome to new first time contributor with code merged to master: vdg0 ([tinydecred](https://github.com/decred/tinydecred/commits?author=vdg0)).

Congratulations to the new contributor listed on [decred.org](https://decred.org/contributors/):

- Amir Massarwa (@amass, Developer)

Community stats as of Jan 3:

- Twitter followers: 40,897 (+256)
- Reddit subscribers: 9,708 (+5)
- Matrix users: 504 (+30)
- Slack users: 6,881 (+9)
- Discord users: 2,628 (+36), verified to post: 407 (+28)
- Telegram users: 2,838 (-65)
- YouTube subscribers: 3,960 (+40)
- Facebook followers: 3,552 (+245), likes: 3,223 (+196)
- LinkedIn followers: 674 (+12)
- GitHub dcrd stars: 528 (+8), forks: 1,458 (+58)

## Governance

In December the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 14,406 DCR and spent 10,106 DCR. Using December's daily average DCR/USD rate of $18.32, this is $264K received and $185K spent. At November's average daily rate of $19.97, the USD figure billed for work completed in that month is $202K. As of Jan 1, Treasury balance is 643,836 DCR (10.9 million USD at $16.87).

December was an unusually quiet month for Politeia, with no new proposals submitted. Two proposals from November were voted on in December:

- The [TinyDecred budget](https://proposals.decred.org/proposals/ad0f9688b3467734e2581604914b2cc32c6eb7991dff460eff41d21f66d88451) proposal was approved with 85% approval and voter participation of 32.6%.
- The [PlusBit POS App](https://proposals.decred.org/proposals/e559188b0febcab29c49c1f7dd5c66645e31be00894a150ef7d0b8ceb6486605) was rejected with 39% approval and participation of 30.6%.

Ditto has submitted their [phase 3](https://proposals.decred.org/proposals/012b4e335f25704e28ef196d650316dca421f730225d39e37b31b3c646eb8497) communications proposal on Jan 7, discussion is ongoing.

Following [analysis](https://www.blockcommons.red/publication/mm-tracking-1/) of the public orderbooks which raised questions about the level of liquidity provision, i2 Trading have provided full trading history logs that will allow for their performance to be scrutinized in detail. Company 0 are working on a set of tools for auditing i2's performance in relation to the criteria specified in their proposal.

Politeia Digest has been taking a break while the level of Politeia activity is low, it will return when new proposals are submitted.

## Network

Hashrate: December's hashrate opened at ~370 Ph/s and closed ~400 Ph/s, bottoming at 275 Ph/s and peaking at 522 Ph/s throughout the month. Pool hashrate distribution as of Jan 2: Poolin 32%, UUPool 24%, lab.antpool.com 12%, F2Pool 2.2%, BTC.com 1.8%, BeePool 0.09%, CoinMine 0.09%, suprnova 0.02%, Luxor 0.02% and others 28% per [dcrstats.com](https://dcrstats.com/pow). Pool distribution numbers are approximate and cannot be accurately determined.

After staying between 400-450 Ph/s in November, in December the hashrate declined further and briefly went below 300 Ph/s (last time it visited this level during a short dip in Apr 2019).

Staking: 30-day average ticket price was 137.5 DCR (+2.7) per dcrstats.com. The price varied between 123.1-158.76 DCR. Locked amount was 5.37-5.61 million DCR, which corresponded to 49.75-51.90% of the available supply.

Once again the ticket price made a new high of 158.76 since the sdiff algorithm change, while 51.9% is the new all-time high of stake participation.

Nodes: Throughout [December](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1575158400000&to=1577836800000) there was an average of 175 public listening nodes and 391 normal nodes per dcr.farm. On average, versions were distributed as: 56% use dcrd v1.4, 10% use dcrd v1.5, 8.8% use dcrd v1.5 dev and RC builds, 6% use dcrwallet v1.4, 1.9% use dcrwallet v1.5.

On [Dec 12](https://twitter.com/lefebvre_dustin/status/1205224368407748616), 16.1% of all DCR in circulation participated in CoinShuffle++ mixing.

Decred mainnet [LN map](https://ln-map.jamieholdstock.com/) shows 11 nodes and 13 channels as of Jan 8.

## Integrations

Welcome to a [new](https://github.com/decred/dcrwebapi/pull/82) VSP [99split.com](https://99split.com/) with a 0.99% fee.

dcr.pos.fans VSP [removed](https://github.com/decred/dcrwebapi/pull/79) from the [listing](https://decred.org/vsp/) since it has proven to be unreliable.

Warning: the authors of Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

Outreach in December featured v1.5.0, with @davecgh educating about consensus changes on both [Decred Assembly](https://www.youtube.com/watch?v=gGQuY0kOt7g) and [Decred in Depth](https://www.youtube.com/watch?v=D1527JwkDrs). The additional episodes of [Decred in Depth](https://www.youtube.com/watch?v=dZeqrQpf-aU) and [Decred Assembly](https://www.youtube.com/watch?v=N3WO5YXpD7M) featured @matheusd on Lightning Network. The copy for the website update was put into GitHub and submitted to the #web\_ops team for assembly. The new site is expected to publish in January.

Much of the rest of the month focused on reflection, discussion, and planning for 2020. @bee's post on [marketing strategies](https://xaur.github.io/writings/posts/20191127-marketing-strategies.html) prompted [a vigorous discussion](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$157617150861861VoZeT:decred.org) in #proposals, as Ditto and @Dustorf look to prepare their next proposals. @Dustorf followed up with [a survey](https://www.surveymonkey.com/results/SM-9JRDSMFS7/) soliciting community input on priorities regarding geographies, market segments, and possible applications. He will also publish a summary of marketing expenditures prior to his next proposal.

Ditto's December achievements:

- Placed CoinDesk Year-in-Review [op-ed](https://www.coindesk.com/its-time-to-walk-the-talk-on-decentralized-governance) by @jy-p about decentralized governance "It's Time to Walk the Talk on Decentralized Governance".
- CoinDesk [article](https://www.coindesk.com/planned-sale-of-org-angers-many-open-source-crypto-developers) on the sale of .org domains, which includes a quote from @richardred.
- Off the Chain [podcast](https://www.youtube.com/watch?v=NNg5G_EZxtU) with Anthony Pompliano and @akinsawyerr, talking about crypto in Africa and Decred's unique governance.
- NasdaqTV TradeTalks [segment](https://www.nasdaq.com/videos/tradetalks%3A-blockchain-emerging-technologies-in-africa) with @akinsawyerr talking about blockchain in Africa.
- Arranged and attended a media tour with @akinsawyerr in NYC, where he met in person with reporters at The Block, Fortune, Pomp's Off the Chain podcast, and the Chain Reaction podcast (pending publication).
- Secured Cigars and Crypto [podcast](https://anchor.fm/investnoir3/episodes/Episode-73---AkinSawyerr-e9pnmu) with @akinsawyerr, which aired on Christmas Day.
- Prepared panel briefing doc and conducted media outreach for @akinsawyerr's participation at the Digital Money Forum at CES (Jan 7). Arranged for him to speak on the "The Libra Effect" [panel](https://thedigitalmoneyforum.com/2020-agenda/), alongside Michael Casey of CoinDesk and Dante Disparte of the Libra Association.
- Spearheaded Decred's most noteworthy achievement of 2019 Twitter [poll](https://twitter.com/decredproject/status/1207060170855141376). The winner was the privacy implementation, with 36.6% of the votes, followed by Politeia & DAO progress (33.1%). 475 people participated in the poll.
- Identified and shared opportunities for the community to engage with Crypto Twitter and educate outsiders about Decred. Lately, the community has been abuzz on the unique contractor model at Decred, particularly for developers. With the community contributing more than 40 unique posts using [#cryptodevs](https://twitter.com/hashtag/cryptodevs) and a new handle [@dcrgoodfirst](https://twitter.com/dcrgoodfirst) as a new aggregate of good first issues for developers interested in contributing to Decred.
- Developed Phase 3 Ditto PR proposal, which will be live on Politeia mid-January.

## Events

Attended:

- Nov 6 - [Bitcoin & Blockchains Meetup](https://www.facebook.com/events/1444182132424731/) - Oaxaca, Mexico. @evok3d represented Decred. ([photos](https://twitter.com/ev0k3d/status/1192945388329807874), _missed in Nov_)
- Dec 4 - [Decred Demo](https://www.meetup.com/blockchaincentre/events/266659342/) - Melbourne, Australia. @eSizeDave and @zohand were invited to present Decred at Blockchain Centre's newly introduced Talk & Trade format. The demo of Politeia and Decrediton was expected to take 30 minutes but the total time surpassed 1.5 hours, which allowed to talk about key aspects of Decred and have a debate among the ~20 participants. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191204-blockchain-centre-talk-and-trade-melbourne-australia.md))
- Dec 7 - Blockchain Communities Meetup - Mexico City, Mexico. Organized by Blockchain Bajio at Bitcoin Embassy Bar. (photos: [1](https://twitter.com/Decred_ES/status/1204144823231488000), [2](https://twitter.com/BlockchainBajio/status/1209141039086362624), [3](https://twitter.com/NancyNSalazar/status/1209143989984808961))
- Dec 12-13 - [Labitconf](https://www.labitconf.com/) - Montevideo, Uruguay. Decred Latam team of 7 people represented the project during 2 days of the event. Previous efforts to build awareness in Latam became evident as many projects attending the event knew about Decred. Having no booth in a single place allowed the team to be everywhere, and they suggest considering this approach for events of this size (~1000 visitors). Check the [full report](https://github.com/decredcommunity/events/blob/master/reports/20191212-labitconf-montevideo-uruguay.md) for notable interactions and other details.
- Dec 15 - [Crypto & Christmas](https://www.meetup.com/blockchaincentre/events/267037974/) - Melbourne, Australia. Decred Australia organized a party together with Blockchain Centre, Cointree and e-Pocket. @eSizeDave and @zohand gave a brief intro to Decred and its achievements to ~20 attendees and used the opportunity to engage with them more directly. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191215-crypto-and-christmas-melbourne-australia.md))
- Dec 20 - [Bitcoin Embassy Anniversary](https://twitter.com/Decred_ES/status/1207380289107959809) - Mexico City, Mexico. Bitcoin Embassy invited Decred Latam team to be present and sponsor the event, thanks to good relationships established earlier. @francov\_, @victorarubin and @luisantoniocrag talked all night about Decred with most of the attendees. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191220-bitcoin-embassy-anniversary-mexico-city-mexico.md))

Upcoming:

- Jan 14 - [GoCracow #7](https://www.meetup.com/en-AU/GoCracow/events/265765051/) - Kraków, Poland. @kozel will present Decred to a Go developer audience and go over some details of working for a DAO and ways of contributing to the project.
- Jan 29-31 - [Crypto 101 Online Summit](https://www.crypto2020summit.com/) - online. @lukebp will give an overview of Decred's plans for 2020.
- Feb 4-6 - Africa Tech Summit - Kigali, Rwanda. @akinsawyerr will be a speaker in the Money & Blockchain Summit.
- Apr 13-17 - Blockchain Land at Talent Land - Guadalajara, Mexico. Decred will be sponsor of Talent Land and be present with a booth at Blockchain Land.
- May, date TBA - [BitConf](https://www.bitconf.com.br/portal/) - São Paulo, Brazil.

## Media

Selected articles:

- Decrediton on Tails by @mm ([stakey.club](https://stakey.club/en/decrediton-on-tails/), also [in Portuguese](https://stakey.club/pt/decrediton-no-tails/), _missed in Nov_)
- Does Decred Have the Answers to On-chain Governance? by Kerman Kohli ([medium](https://medium.com/decred/does-decred-have-the-answers-to-on-chain-governance-d35bdd176f59), _missed in Nov_)
- Decred On-chain: The Ticket Pool VWAP by @permabullnino ([medium](https://medium.com/@permabullnino/decred-on-chain-the-ticket-pool-vwap-d0a3d1c42a3))
- Overview of 'Staking' in a Variety of Projects by @richardred ([blockcommons.red](https://www.blockcommons.red/publication/staking/))
- It's Time to Walk-the-Talk on Decentralized Governance by @jy-p, part of CoinDesk's year in review ([coindesk](https://www.coindesk.com/its-time-to-walk-the-talk-on-decentralized-governance))
- Introducing DownloadHawk by @degeri ([blog.decred.org](https://blog.decred.org/2019/12/16/Introducing-DownloadHawk/))

Translations:

- My experience setting up a Decred full-node - [in Spanish](https://medium.com/decred-es/mi-experiencia-configurando-un-nodo-completo-de-decred-d5321304bc48) by @pablito
- Decred Journal - November 2019 was translated to Arabic (@arij), Chinese (@Dominic), Spanish (@luisantoniocrag and @francov\_), and Polish (@kozel). Thank you all!

Videos:

- Decred Assembly Deep Dive - Lightning Network with @matheusd ([youtube](https://www.youtube.com/watch?v=N3WO5YXpD7M))
- TradeTalks: Blockchain & Emerging Technologies in Africa. @akinsawyerr talks about the importance of governance for crypto's prospects in Africa. ([nasdaq.com](https://www.nasdaq.com/videos/tradetalks%3A-blockchain-emerging-technologies-in-africa))

Audio:

- POV Crypto 105 - Fight Night XI: BTC vs ETH vs DCR, with @Checkmate. An in depth debate of the Bitcoin, Ethereum and Decred perspectives on a variety of blockchain subjects. ([youtube](https://www.youtube.com/watch?v=7m1kfM0fqaE))
- Decred in Depth Ep. 15 features @davecgh giving an in depth overview of v1.5 and the block header commitments consensus rule change proposal. Dave covers the detail of what the proposal involves, and the ways in which it will enhance the network if approved. ([youtube](https://www.youtube.com/watch?v=D1527JwkDrs), [soundcloud](https://soundcloud.com/decredindepth/ep-15-dave-collins-btc-suite-origins-dcrd-15))
- Decred in Depth Ep. 14 - @matheusd talks about getting into Lightning Network development through his work on ticket-splitting, the challenges of porting Lightning Labs' lnd to Decred, and the various ways in which the basis in btcd helps. ([youtube](https://www.youtube.com/watch?v=dZeqrQpf-aU), [soundcloud](https://soundcloud.com/decredindepth/ep-14-matheus-degiovani-dcr-lightning-network))
- Off the Chain - How Crypto is Bridging the Gap Between the Banked and Unbanked. @akinsawyerr has an extensive interview with Anthony Pompliano about cryptocurrency and Africa. ([youtube](https://www.youtube.com/watch?v=NNg5G_EZxtU), [spotify](https://open.spotify.com/episode/1FGOnQb84YpGTZfwbEzdAg))
- Cigars and Crypto 73 - @akinsawyerr talks about Africa and Decred. ([anchor.fm](https://anchor.fm/investnoir3/episodes/Episode-73---AkinSawyerr-e9pnmu))

Decred bullish sentiment hit a yearly high, according to [LunarCRUSH](https://twitter.com/LunarCRUSH/status/1208975910013026304).

@AGNFAB1 posted [more](https://www.reddit.com/r/decred/comments/eevd8f/decred/) of his Decred art. Previous works: [Christmas](https://twitter.com/AGNFAB1/status/1208044700634157056), [Banking on Decred](https://twitter.com/AGNFAB1/status/1199788339404181504), [Tacotime Trilogy](https://www.reddit.com/r/Monero/comments/dzh6vr/tacotime_trilogy/), [Decentralized Credits](https://www.reddit.com/r/decred/comments/dqocpf/decentralized_credits/).

## Community Discussions

Selected Reddit posts:

- This [post](https://www.reddit.com/r/decred/comments/ecvjaj/the_decred_security_curve_you_want_to_double/) linking to a Twitter thread about Decred's security attracted 39 comments in which one user argued at length that exchanges could execute an attack where they drained the Treasury.
- This [post](https://www.reddit.com/r/decred/comments/e8v7pd/other_than_staking_sending_to_exchanges_what/) asked what people use Decred for other than staking and sending to exchanges.

Selected Twitter action:

- A @decredproject [poll](https://twitter.com/decredproject/status/1207060170855141376) asking about the most noteworthy achievement of 2019 had 475 responses. 37% went for Privacy, 33% for Politeia/DAO, 19% for Lightning Network and 11% for DEX.
- Merry [Stakemas](https://twitter.com/DCRComic/status/1209541923737886721) from @DCRComic.
- @buck54321's [campaign](https://twitter.com/blockchainbuck/status/1201988834575224832) for the TinyDecred proposal targeted older voters.
- @Exitus [tweeting](https://twitter.com/coveryfire7777/status/1208499268987867138) about v1.5 Dark Mode.
- @Dustorf's [year](https://twitter.com/lefebvre_dustin/status/1207756052382593026) in Decred.
- @ammarooni's [thread](https://twitter.com/Ammarooni/status/1208060799736004611) about Decred as Bitcoin's younger sibling.

DCRComic:

- [DEX](https://twitter.com/DCRComic/status/1211672109321248768).
- [Ticket Rick](https://twitter.com/DCRComic/status/1204049820350111744) - a reference to Pickle Rick from the Rick & Morty animated show.
- [Collective Intelligence](https://twitter.com/DCRComic/status/1202601872919543811).

Chats:

- Heating [chicken coops](https://matrix.to/#/!NNzHoaSdnsbZDQOXJr:decred.org/$157534140455245zYGLX:decred.org) and mushroom farms with DCR mining rigs.

## Markets

In December DCR was trading between USD 15.61-20.77 / BTC 0.0023-0.0029. The average daily rate was $18.32.

## Relevant External

A [spec](https://stratumprotocol.org/) for the Stratum V2 mining protocol was published by Braiins in November, following the summer announcement. The new protocol addresses many issues in V1 and provides more efficient and secure communication between the hashing miners and the pool. A big feature of V2 is a new mode where miners choose transactions and version bits to include in the block, removing this power from the pool. This mode will be optional and [will not be](https://twitter.com/mor_pav/status/1194725696817553410) the default to avoid harming adoption. Joined by Matt Corallo and Peter Todd, Braiins hosted a comprehensive [AMA](https://www.reddit.com/r/Bitcoin/comments/dz1mgp/ama_bitcoin_mining_stratum_v2_we_are_braiins_the/) on Reddit.

VTC [suffered](https://cryptobriefing.com/vertcoin-51-attacked-once-again/) another 51% attack and a 600 block reorg, but this time it appears that the attackers probably failed to profit from the attack as Bittrex (the likely target) disabled trading as soon as it was detected.

The Wharton Cryptogovernance Workshop [launched](https://twitter.com/ProfPieters/status/1205219084528431113) cryptogov.net, which includes "[Governance Assessments](https://cryptogov.net/view-responses-by-question/)", self-assessed answers to a standard set of questions about blockchain governance, compiled by members of the different projects. Decred was one of 3 projects to have its [answers](https://cryptogov.net/participating-projects/entry/14/) uploaded ahead of the launch. @akinsawyerr attended an [event](https://twitter.com/kwerb/status/1146505123876802564) at Wharton in Jul 2019 where the project was instigated, and also took the lead on preparing Decred's answers, with some assistance from @richardred.

The results of the Zcash community sentiment polling were [released](https://www.zfnd.org/blog/community-sentiment-collection-results/). Participants were the community advisory panel and forum users, none of the PoW miners chose to signal using the polling method offered to them. Voters could signal support for all 13 proposals by voting Yes/No on each one.

There was very little support for proposals that did not continue to dedicate 20% of the block reward to development funding.

48 of the 62 Community Advisory Panel members responded to the poll. Options #12 (60% split between EFF/Zfnd, 40% to a major grants program with extra advisors) and #10 (The "grand compromise", similar distribution to #12) did well with close to 75% support. Option #13 ("Keep it simple", 50% split ECC/Zfnd) also got >50% approval.

77 forum users (of 104 eligible) voted on the proposals (accounts created after March 2019 were not eligible). #12 did the best among this group with 70% approval, #13 also did well with over 50% support.

1% of all the circulating ZEC [voted](https://twitter.com/zooko/status/1200917828011876352) in the unofficial stake-weighted poll, the most popular options within this constituency were #10 and #8 (just 2 more years of 20% funding for ECC).

The Zcash Foundation decided to develop option #12 with some improvements, then rolled [back](https://www.zfnd.org/blog/proposed-nu4-zip/) on most of the improvements in response to pushback. The final slightly amended version of the proposal will be put to another community panel and forum user vote to confirm it.

[ZIP 1012](https://github.com/ZcashFoundation/zips/blob/master/zip-1012.rst), as it has become, involves extending the block reward for 4 years at 20%, with 35% going to ECC, 25% to Zfnd, and 40% for additional "Major Grants". Changes to the proposal involve making it more directly controlled by Zfnd, and removing a restriction that would have excluded ECC from receiving any funding as part of "major grants". Another change added to the proposal by Zfnd is to "Call for, and incentivize, development of decentralized voting and governance".

The Zcash Foundation also [donated](https://www.coindesk.com/zcash-foundation-funds-app-mixing-private-messaging-and-payments) $40,000 to Open Privacy for development of [Cwtch](https://openprivacy.ca/work/cwtch/), a decentralized messaging and payments platform.

IOTA got itself in a tangle and was [halted](https://cryptobriefing.com/iota-halts-15-hours-from-coordinator-bug/) for 15 hours due to a bug with the Coordinator.

Jack Dorsey of Twitter [announced](https://twitter.com/jack/status/1204766078468911106) that Twitter would fund research into a decentralized version of its platform.

Moocowmoo, a Dash Core advisor and provider of a custodial master node shares service, [disappeared](https://bitcoinist.com/making-a-dash-for-it-moocowmoo-disappears/) while in the process of winding down the service, leaving some clients waiting for their DASH back for an extended period. After the increase in attention, Moocowmoo re-surfaced and the DASH [began](https://bitcoinist.com/dash-investors-funds-returned-moocowmoo-awakes/) to flow back to its rightful owners within a week.

Bitfinex [announced](https://www.theblockcrypto.com/linked/48976/bitfinex-to-support-deposits-and-withdrawals-on-lightning-network) that it would begin supporting Lightning Network deposits and withdrawals starting Dec 3.

Etherscan.io, a popular Ethereum block explorer, was [blocked](https://www.coindesk.com/chinas-internet-firewall-has-blocked-access-to-ethereum-block-explorer-etherscan-io) by the Chinese Great Firewall. No reasons were given, other block explorers remain accessible.

Google [banned](https://news.bitcoin.com/google-bans-crypto-app-metamask-from-play-store/) Metamask, a browser app for interacting with Dapps, from its Play Store, for allegedly doing covert mining. While their appeal was initially [rejected](https://twitter.com/metamask_io/status/1210299207820570624), the ban was [overturned](https://thenextweb.com/hardfork/2020/01/03/google-lifts-ban-ethereum-wallet-app-metamask-mining-cryptocurrency/) a few days later.

Google also purged a lot of crypto-related videos on YouTube, before reinstating them after deciding it was an [error](https://www.bbc.co.uk/news/technology-50924494). The incident apparently left many affected YouTube content producers [looking](https://news.bitcoin.com/youtube-christmas-purge-has-content-creators-pointing-to-these-alternate-platforms/) at the decentralized alternatives available to them.

A Cryptocurrency Anti-Money Laundering [Report](https://ciphertrace.com/wp-content/uploads/2019/11/CipherTrace-Cryptocurrency-Anti-Money-Laundering-Report-2019-Q3.pdf) from CipherTrace mentioned Decred as a cryptocurrency with privacy features.

The Stellar airdrop on Keybase has been [ended](https://keybase.io/a/i/r/d/r/o/p/spacedrop2019) prematurely due to a sharp increase in junk sign-ups, with 100,000 accounts being excluded and the final allocation of Lumens being divided between 282,000 users.

The /r/ethtrader donuts experiment continued with the [launch](https://new.reddit.com/r/ethtrader/comments/eckj24/ethtrader_special_membership_is_now_live/) of a special membership where members can pay a monthly subscription of 5,000 donuts to unlock features like name badges and the privilege to post gifs in comments.

The Maker Foundation [sold](https://www.theblockcrypto.com/post/51059/makerdao-receives-27-5m-from-dragonfly-and-paradigm-to-expand-into-asia) 5.5% of the total MKR supply to Dragonfly Capital and Paradigm for $27.5 million in a bespoke arrangement that will see MKR put more emphasis on the Asian market.

Months after launching a custodial staking service for Tezos, the Coinbase exchange is [now](https://twitter.com/brian_armstrong/status/1207818862768480256) the #1 baker on the XTZ network.

"MetaCartel", an effort to create a for-profit investment DAO in the mold of the original and infamous DAO but built on the complexity-averse Moloch, released a [white paper](https://github.com/metacartel/MCV/blob/master/Whitepaper.pdf). Moloch DAO [announced](https://twitter.com/ameensol/status/1212475508262363137) an update to v2 which facilitates pairing Moloch with a legal entity without violating securities regulations.

Algorand relay nodes voted to [accept](https://algorand.foundation/long-term-vesting-plan-vote-result) an [amendment](https://algorandfoundation.cdn.prismic.io/algorandfoundation/eb2a8c69-2262-42f8-99a4-09df485207b5_EIP-11252019AF_+Conditional+Accelerated+Vesting+Nov+30.pdf) to the vesting schedule of the tokens they received as grants from the Algorand Foundation. This amendment increases the number of Algo tokens relay nodes will receive by 25%, but extends the vesting schedule from 2 to 5 years, with a mechanism to speed it up if the Algo price rises. This concludes an [episode](https://algorand.foundation/voting-procedure-eip09092019pc) which started and was missed in Sep, with relay nodes voting to suspend their own rewards until a change to the vesting schedule could be agreed.

There are around 81 Algorand relay nodes and these proposals were approved with yes votes from around 55 nodes (plus many abstentions and a few no votes). The Algorand nodes have completed KYC/AML checks and entered into a legal agreement with the foundation, such that part of the voting process for these proposals involved using DocuSign to sign and return copies of the amendment to the Foundation. KYC/AML checks are also [mandatory](https://algorand.foundation/200millionalgo-staking-rewards-kyc-extended) for Algo holders who wish to participate in staking and receive rewards.

A new [attack](https://arstechnica.com/information-technology/2020/01/pgp-keys-software-security-and-much-more-threatened-by-new-sha1-exploit/) on SHA-1 hash function published early January has a practical application of impersonating PGP/GnuPG users and signing any document in their name. The attack cost is estimated $45,000 and will decrease as computation gets cheaper. If you use GnuPG, configure it to not use SHA-1 for signatures or upgrade to 2.2.18+. Signatures for Decred [v1.5.0 release](https://github.com/decred/decred-binaries/releases/tag/v1.5.0) are not affected since they use SHA-256.

## About This Issue

This is issue 21 of Decred Journal. Index of all issues, mirrors and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: akinsawyerr, bee, Dustorf, degeri, fguisso, kozel, margaret\_mei, richardred, s\_ben
- reviews and feedback: buck54321, chappjc, Checkmate, davecgh, dnldd, lukebp, matheusd, raedah
- title image: saender

