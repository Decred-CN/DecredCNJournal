# Decred Journal – May 2020

![abstract art](img/journal-202005-384.png)

_Image: Ascending Bits by @saender_

May's highlights:

- The new vspd software was introduced, this will replace the existing dcrstakepool software used by VSP operators, and significantly improve the VSP staking experience for all users once v1.6 is released by eliminating the requirement for VSP user accounts.
- The Decred DEX software is in open testing, if you're feeling adventurous why not atomic swap some testnet credits?
- Significant new components of Politeia are falling into place, RFP proposals and on the CMS side all-contractor voting functionality.
- Test builds of the v1.5 updates for both mobile apps are now available through the respective app stores - testers are very welcome to submit issues on GitHub.

## Development

Unless otherwise noted, the work reported here has the "merged to master" status. It means that the work is completed, reviewed, and integrated into the source code that advanced users can build and run, but is not yet available in release binaries for regular users.

[dcrd](https://github.com/decred/dcrd):

- reworked HTTPS [seeding](https://github.com/decred/dcrd/pull/2188) (for reference, the network is [migrating](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$156556717014681nMMAT:decred.org) to seeding over HTTPS because it is more secure, does not require a large dependency surface like DNSSEC, and is more flexible)
- [banning](https://github.com/decred/dcrd/pull/2110) peers that don't follow the wire protocol
- more code migrated to the Go 1.13 error handling

In progress:

- TSPEND opcode needed for decentralized control of the Treasury by the stakeholders was successfully [tested](https://twitter.com/marco_peereboom/status/1263185839028350976) on testnet

[dcrwallet](https://github.com/decred/dcrwallet):

- added client [package](https://github.com/decred/dcrwallet/pull/1726) for JSON-RPC calls
- ability to request multiple blocks from the same peer [concurrently](https://github.com/decred/dcrwallet/pull/1730) (one of the needed changes for SPV support in dcrlnd)
- ability to save [per-ticket](https://github.com/decred/dcrwallet/pull/1737) vote preferences (step towards ticket-based VSP)

In progress:

- [hardened](https://github.com/decred/dcrwallet/pull/1743) account support for ticket-based VSP API

[Decrediton](https://github.com/decred/decrediton):

- code refactoring, more components reused from pi-ui
- codebase [prettified](https://github.com/decred/decrediton/pull/2481) with automated rules to improve readability
- UI tweaks

In progress:

- [mixed](https://twitter.com/_vctt/status/1265397168317366283) transactions

[Politeia](https://github.com/decred/politeia):

- RFP process implemented in the [backend](https://github.com/decred/politeia/pull/1054) and the [GUI](https://github.com/decred/politeiagui/pull/1910) - a big change in development for a long time, has been implemented and is in testing
- admin utility to [change email](https://github.com/decred/politeia/pull/1178) address
- [short URLs](https://github.com/decred/politeia/issues/900) for proposals
- arrow key [navigation](https://github.com/decred/politeiagui/pull/1878) for attached images
- progress towards viewing Politeia with [no javascript](https://github.com/decred/politeiagui/pull/1834)
- two temporary workarounds were implemented to mitigate the annoying duplicate comments bug: one where the expensive file system check is run [once a day](https://github.com/decred/politeia/pull/1205) instead of once an hour, and another where commenting is temporarily [blocked](https://github.com/decred/politeiagui/pull/1944) during the time when the bug would be triggered
- lots of bug fixes

CMS:

- [all-contractor](https://github.com/decred/politeia/pull/1104) vote for contentious DCCs, weighted by the number of billed hours over the previous 6 months - the final part of implementing the DCC process [proposal](https://proposals.decred.org/proposals/fa38a3593d9a3f6cb2478a24c25114f5097c572f6dadf24c78bb521ed10992a4)
- [utility](https://github.com/decred/politeia/pull/1179) to test DCC issuance and DCC vote processes

In progress:

- admin feature to query [code stats](https://github.com/decred/politeia/pull/1185) for contractors

[vspd](https://github.com/decred/vspd):

vspd is a from-scratch implementation of VSP software that will bring a huge improvement to the privacy of VSP users, and by extension, the security of the Decred network. It will also be much easier to use for having no registration, no emails, no CAPTCHAs, and no redeem scripts to back up. Check the [announcement](https://blog.decred.org/2020/06/02/A-More-Private-Way-to-Stake/) for more details.

[MVP](https://en.wikipedia.org/wiki/Minimum_viable_product) for vspd is nearing completion and dcrwallet integration is starting. The only outstanding feature for MVP is to get cross-wallet consistency checks to ensure all wallets are voting on the right tickets, and with the right voting choices.

[dcrpool](https://github.com/decred/dcrpool):

v1.1 release candidate is ready for testing! This release includes [reworked](https://github.com/decred/dcrpool/pull/207) payments processing, refreshed UI/UX, higher efficiency via dcrd's work notifications, and a host of smaller improvements and bug fixes. Check the full [release notes](https://github.com/decred/dcrpool/releases/tag/v1.1.0-rc1) for details.

[dcrlnd](https://github.com/decred/dcrlnd):

@matheusd posted a [demo](https://twitter.com/matheusd_tech/status/1263118566418776065) of swapping between BTC and DCR invoices across their respective LNs. This is effectively an "instant exchange", except it is using LN and is non-custodial. Note that this prototype has a known gaming vector and more R&D is required to resolve it (ideally based on [PTLCs](https://suredbits.com/payment-points-monotone-access-structures/), but it is quite far away in the future). More details in [this chat](https://matrix.to/#/!LtiDnUlfuRJMekjFSx:decred.org/$ILkQ49LXwBrUcMq5R_JRIkTcjR7FG9lxwMWsxDve2K0).

[dcrdex](https://github.com/decred/dcrdex):

- more secure [handling](https://github.com/decred/dcrdex/pull/291) of encryption password
- overhaul of client wallet configuration, allowing the user to specify a wallet config file or manually enter settings (parts: [1](https://github.com/decred/dcrdex/pull/311), [2](https://github.com/decred/dcrdex/pull/335), [3](https://github.com/decred/dcrdex/pull/346), [4](https://github.com/decred/dcrdex/pull/352))
- server support for graceful [trade suspension](https://github.com/decred/dcrdex/pull/287) and client notifications that are used for planned maintenance and market reconfiguration
- [expanded](https://github.com/decred/dcrdex/pull/378) "Your Orders" table in client's browser interface
- [display](https://github.com/decred/dcrdex/pull/348) of epoch (pending) limit orders on depth chart as a separate dashed line. Epoch orders are orders that have been submitted, but yet to be processed by the order matching algorithm. This provides a preview of how the market is changing during an open epoch, which is on the order of 10 seconds. 
- client [balance update](https://github.com/decred/dcrdex/pull/418) improvements to give a more up-to-date balance value
- [Litecoin support](https://github.com/decred/dcrdex/pull/372) for the client. LTC was already supported by the server, dcrdex, but now the client can use LTC wallets and place orders for LTC markets.
- [trade command](https://github.com/decred/dcrdex/pull/315) to allow placing trades from the command line
- [exchanges command](https://github.com/decred/dcrdex/pull/314) to allow listing and configuring exchanges from the command line
- market [search box](https://github.com/decred/dcrdex/pull/426) to the Markets page of the client's browser interface
- improved [notification](https://github.com/decred/dcrdex/pull/343) of registration events (e.g. fee payment confirmations completed)
- [sign out](https://github.com/decred/dcrdex/pull/347) action
- multiple bug fixes and code refactoring

A total of 59 PRs from 10 contributors were [merged](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-05-01..2020-05-31+sort%3Aupdated-asc), adding 10K and deleting 3K lines of code.

Upcoming work includes: Server support for suspend/restore active swaps (swap state), better support for client-initiated refund or swap completion (refund) in the event of failure of the server-driven swap negotiation due to a down server or counter party inaction, expanded client RPCs, expanded server admin commands, improved client handling of server suspend/resume messages.

Testnet testing [has begun](https://twitter.com/chappjc/status/1267115398610255874) and everybody is welcome to [participate](https://github.com/decred/dcrdex/wiki/Testnet-Testing). There's still a good chance that mainnet DEX will launch this summer.

[dcrandroid](https://github.com/decred/dcrandroid):

- [watch-only](https://github.com/decred/dcrandroid/pull/471) wallet support
- [encrypt](https://github.com/raedahgroup/dcrlibwallet/pull/131) wallet seed and tighten up the privacy of [seed entry](https://github.com/decred/dcrandroid/pull/473) (_privacy [concerns](https://github.com/decred/dcrandroid/issues/351) around Google Keyboard - who would have thought_)
- request [passphrase](https://github.com/decred/dcrandroid/pull/467) before showing or verifying seed
- [limit](https://github.com/decred/dcrandroid/pull/472) user to 1 wallet per 1 GB of RAM
- [Polish](https://github.com/decred/dcrandroid/pull/405) translation
- multiple bug fixes

Testnet build of the v1.5 release is available on [Google Play](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.testnet). Bug reports are welcome on [GitHub](https://github.com/decred/dcrandroid/issues).

[dcrios](https://github.com/raedahgroup/dcrios):

- [watch-only](https://github.com/raedahgroup/dcrios/pull/685) wallet support
- blockchain [rescan](https://github.com/raedahgroup/dcrios/pull/675) implemented
- Decred [logo](https://github.com/raedahgroup/dcrios/pull/674) on QR codes
- [Polish](https://github.com/raedahgroup/dcrios/pull/683) translation ported from Android
- multiple bug fixes

Testnet build of the v1.5 release is available on [Apple TestFlight](https://testflight.apple.com/join/7KL4VnB2). Bug reports are welcome on [GitHub](https://github.com/raedahgroup/dcrios/issues).

[dcrdata](https://github.com/decred/dcrdata):

- attack cost page now takes [circulating DCR](https://github.com/decred/dcrdata/pull/1736) into consideration
- v5.3 beta is [deployed](https://twitter.com/decredexplorer/status/1262827698986127360) to [main site](https://dcrdata.decred.org/)

In progress:

- DCR price increase [prediction](https://github.com/decred/dcrdata/pull/1738) on the attack cost page, based on the current order books on exchanges (WIP version deployed at [planetdecred.org](https://explorer.planetdecred.org/attack-cost) for testing)
- display Swap Contract and Swap Redemption labels for [atomic swap](https://github.com/decred/dcrdata/pull/1733) transactions
- [/nextreduction](https://github.com/decred/dcrdata/pull/1753) page with a countdown till next block reward reduction and basic information about it (a fun entry point to share with people learning about Decred)

[tinydecred](https://github.com/decred/tinydecred):

- foundations for [SPV peer](https://github.com/decred/tinydecred/pulls?q=is%3Apr+merged%3A2020-05-01..2020-05-31+sort%3Aupdated-asc+spv) support
- added BTC network [parameters](https://github.com/decred/tinydecred/pull/184) (first step for multi-asset support)
- tooling to measure [test coverage](https://github.com/decred/tinydecred/pull/180)
- [v0.1.0](https://github.com/decred/tinydecred/releases/tag/v0.1.0) is the first tagged release (_congrats!_)

[docs](https://github.com/decred/dcrdocs):

- [overhauled](https://github.com/decred/dcrdocs/pull/1090) the [Verifying Binaries](https://docs.decred.org/advanced/verifying-binaries/) page which now explains what the user needs to do and why, updated multiple pages to [encourage](https://github.com/decred/dcrdocs/pull/1094) users to verify binaries (_you should too!_)
- [added](https://github.com/decred/dcrdocs/pull/1089) new [Redeem Script](https://docs.decred.org/proof-of-stake/redeem-script/) page that explains what it is, backup, and recovery

Other:

- @mm published [InvalidationGame](https://github.com/mmartins000/invalidationgame), a script that simulates a double-spending attack on a simulated pure PoW network, or a hybrid PoW+PoS network like Decred.
- Bug Bounty website posted a new [update](https://bounty.decred.org/2020/05/status-update/): a total of 123 submissions have been processed (+19), with 13 of them being eligible for a payout (+2).
- Some developers are more active on Twitter now with the dev updates. You can follow [@lukebp_](https://twitter.com/lukebp_), [@marco_peereboom](https://twitter.com/marco_peereboom), [@degeri_crypto](https://twitter.com/degeri_crypto), and others to get more of those. If you are a developer with a Twitter account, you can help to spread the builder culture of Decred by tweeting such dev updates (and don't hesitate to suggest them for a retweet in [#media](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org)!).

Dev activity stats for May (approximate): ~300 active PRs, ~340 master commits, ~51K added and ~26K deleted lines spread across 16 repositories (note: line counts exclude Decrediton [#2481](https://github.com/decred/decrediton/pull/2481) that reformatted a huge repository). Contributions came from 2-10 developers per repository.

## People

Welcome to new first time contributors with code merged to master: @blaltarriba ([politeiagui](https://github.com/decred/politeiagui/commits?author=blaltarriba)), @dreacot ([dcrandroid](https://github.com/decred/dcrandroid/commits?author=dreacot)), @Ekeh ([dcrdata](https://github.com/decred/dcrdata/commits?author=Ekeh)), @guilhermemntt ([decrediton](https://github.com/decred/decrediton/commits?author=guilhermemntt)), @rstaudt2 ([dcrd](https://github.com/decred/dcrd/commits?author=rstaudt2)) and @song50119 ([dcrdex](https://github.com/decred/dcrdex/commits?author=song50119)).

Congratulations to new contractors granted the Decred Contractor Clearance (DCC): [@camilolwi](https://twitter.com/Camilolwi) (marketing), [@itswisdomagain](https://github.com/itswisdomagain) (development), [@nachito](https://github.com/Reidiojed) (marketing), [@tomee](https://twitter.com/tomasgroos) (marketing).

Three Decred community members were [included](https://twitter.com/Decred_BR/status/1262454667700768769) in the list of top 50 names in the Brazilian Crypto Market by Cointelegraph: Rafaela Romano in #35, Gabriel Rhama in #31 and the number one Edilson Osório Jr.

Community stats as of Jun 1:

- Twitter followers: 40,492 (-78)
- Reddit subscribers: 9,792 (+31)
- Matrix users: 655 (+31)
- Discord users: 1,222 (+38)
- Telegram users: 2,603 (+46)
- YouTube subscribers: 4,030 (+40), views: 144K (+3.5K since May 8) 
- Facebook followers: 3,632 (+14), likes: 3,291 (+11)
- LinkedIn followers: 810 (+36)
- GitHub dcrd stars: 543 (+4), forks: 240 (+5)

## Governance

In May the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 13,594 DCR and spent 19,153 DCR. Using May's daily average DCR/USD rate of $14.11, this is $192K received and $270K spent. At April's average daily rate of $12.34, the USD figure billed for work completed in that month is $236K. As of Jun 5, Treasury balance is 630,983 DCR (11.4 million USD at $18.12).

There were 5 proposals submitted in May, and 4 of these started voting in early Jun. There was no Politeia proposal voting in May.

The new proposals are described in [issue 31](https://blockcommons.red/politeia-digest/issue031/) of Politeia Digest and the vote outcomes will be covered in the next issue.

## Network

Hashrate: [May's hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=k9nb7wvw-kavn2b1a&scale=linear&bin=block&axis=time) opened at ~357 Ph/s and closed ~386 Ph/s, bottoming at 260 Ph/s and peaking at 541 Ph/s throughout the month. Pool [hashrate distribution](https://dcrstats.com/pow) as of Jun 1 (approximate): UUPool 38%, Poolin 18%, lab.antpool.com 12%, F2Pool 1.5%, Luxor 1.3%, BTC.com 1.3%, BeePool 0.1%, CoinMine 0.03%, Suprnova 0.02% and others ~28%.

Staking: [30-day average](https://dcrstats.com/) ticket price was 141.5 DCR (+3.7). The [price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=k9nb7wvw-kavn2b1a&bin=window&axis=time&visibility=true-false&mode=stepped) varied between 132.9-159.2 DCR. [Locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=k9nb7wvw-kavn2b1a&scale=linear&bin=block&axis=time) was 5.59-5.80 million DCR, which corresponded to 48.7-50.3% of the available supply [participating](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=k9nb7wvw-kavn2b1a&scale=linear&bin=block&axis=time) in PoS.

Nodes: Throughout [May](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1588291200000&to=1590969600000) there was an average of 144 public listening nodes and 229 total nodes per dcr.farm. Average version distribution for May: 48% dcrd v1.5.1, 11% dcrd v1.5.0, 6% dcrd v1.6 dev builds, 4% dcrd v1.5 dev and RC builds, 2% dcrd v1.4, 9% dcrwallet v1.5.1, 1.4% dcrwallet v1.5, 1.4% dcrwallet v1.4, and 13% others.

Lewis Harland published a piece of [research](https://formalverification.substack.com/p/in-the-network-decred) about the Decred network that considers a number of metrics, including the ratio of hashrate to USD block reward which represents miners' risk. It notes a decline of several metrics since Jan 2020 and suggests that DCR is trading at a loss relative to the total USD input to the network.

@PermabullNino released another on-chain [research piece](https://medium.com/@permabullnino/decred-on-chain-mining-pulse-3b28d5155a04) where he explores Decred block times and introduces the Mining Pulse indicator.

## Integrations

[Transak](https://global.transak.com/) brought a new way to purchase DCR with a debit card for residents of the US, EU, and many other countries, thanks to a [partnership](https://twitter.com/transak_finance/status/1265690509844131846) with Wyre. "Transak uses smart contracts to connect the end-user to liquidity on centralized and decentralized exchanges. Users will have to input simple KYC information, but the process from start to finish will take less than 5 minutes". Now Transak is live in 32 countries, supporting 14 fiat currencies and 300+ cryptoassets.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

Decred was present at the Consensus: Distributed virtual event where 6 community members delivered 4 sessions, all of which are on YouTube now. Besides this event that was based in USA, all other (known) events in May were targeting the Latam/Brazil region.

Decred in Depth and Rough Consensus podcasts published a total of 4 new episodes.

After starting his Medium [blog](https://medium.com/@Phoenixgreen) in April, Phoenix Green expanded to YouTube video creation and as of writing his [channel](https://www.youtube.com/channel/UCZSFAqUMp8v58eEQl_bzWYg) has 10 videos about Decred. Congrats on the launch and keep up the original quality content!

Monde PR's achievements for May: 

- created and pitched 3 story ideas to investing, finance and crypto publications
- submitted comments from Decred spokespeople to 7 news stories
- secured one media interview and one email Q&A with crypto publications

News coverage secured by Monde PR:

- an article in [Forbes](https://www.forbes.com/sites/cbovaird/2020/05/05/is-this-the-perfect-time-for-central-bank-digital-currencies/) featuring commentary by @jy-p on CBDC privacy concerns 
- an article in [Cointelegraph](https://cointelegraph.com/news/bitcoin-s-halving-incentivizes-miners-to-sell-for-double-decred-co-founder-says) featuring commentary by @jy-p on the impact of Bitcoin's halving, syndicated to 12 news outlets including [FXStreet](https://www.fxstreet.com/cryptocurrencies/news/decred-co-founder-expects-bitcoin-halving-to-spike-btcs-price-202005070208). The comments were also included in a [Zero Hedge](https://www.zerohedge.com/markets/paul-tudor-jones-buys-bitcoin-hedge-against-central-bank-money-printing) article and a second story in [Cointelegraph](https://cointelegraph.com/news/top-experts-make-bitcoin-price-predictions-as-btc-halving-approaches), syndicated to 12 news outlets including [Miami Diario](https://miamidiario.com/bitcoin-a-la-mitad-los-expertos-creen-que-solo-se-debe-comprar-si-se-retiene-a-largo-plazo/) and [Crypto News Australia](https://cryptonews.com.au/story/top-experts-make-bitcoin-price-predictions-as-btc-halving-approaches-121382).
- an article in [Finance Magnates](https://www.financemagnates.com/cryptocurrency/news/will-the-upcoming-halving-increase-bitcoins-price/) featuring commentary from @raedah on Bitcoin's halving. @raedah's comments were also included in a second [Finance Magnates](https://www.financemagnates.com/cryptocurrency/news/will-the-bitcoin-halving-kill-independent-miners/) article on this topic. 
- an article in [Cointelegraph](https://cointelegraph.com/news/stairway-to-scarcity-bitcoin-sentiment-to-rise-despite-halving-impact) featuring commentary from @Checkmate on Bitcoin's halving, syndicated to 5 news outlets including [Investing.com](https://www.investing.com/news/cryptocurrency-news/stairway-to-scarcity-bitcoin-sentiment-to-rise-despite-halving-impact-2164431)
- an article in [Reuters](https://www.reuters.com/article/crypto-currencies-bitcoin/as-pandemic-rages-anything-goes-for-bitcoins-third-halving-idUSL1N2CP13B) featuring commentary from @jy-p, syndicated to 70 news outlets including [The New York Times](https://www.nytimes.com/reuters/2020/05/08/business/08reuters-crypto-currencies-bitcoin.html) (now removed), [Business Insider](https://www.businessinsider.com/as-pandemic-rages-anything-goes-for-bitcoins-third-halving-2020-5) and [Nasdaq](https://www.nasdaq.com/articles/as-pandemic-rages-anything-goes-for-bitcoins-third-halving-2020-05-08). @jy-p's comments were also picked up in subsequent articles about the halving in [Yahoo Finance](https://finance.yahoo.com/news/bitcoin-halved-price-165148071.html), [CryptoSlate](https://cryptoslate.com/bitcoin-goes-through-the-most-brutal-halving-ever-recorded-heres-why/) and [msn.com](https://www.msn.com/en-us/money/markets/demand-for-bitcoin-surges-as-halving-countdown-approaches/ar-BB13RavI).
- an article in [8btc.com](https://m.8btc.com/article/594407) featuring commentary from @jy-p on Bitcoin's halving 
- an article in [Cointelegraph](https://cointelegraph.com/news/bitcoin-halving-was-not-the-apocalyptic-event-some-in-crypto-feared) featuring commentary from @Checkmate on Bitcoin's halving
- an article in [AMB Crypto](https://eng.ambcrypto.com/xrp-trades-wide-as-iota-decred-look-to-make-room/) featuring commentary from @jy-p on CBDCs
- in total 123 articles appeared across 21 countries in May from the above efforts, see full list [here](https://docs.google.com/spreadsheets/d/1oef5U9R_JZ7hxmRRNKDCQNia7u-1lRuGk6w3w3LU-p0/edit?usp=sharing)

## Events

Attended:

- Apr 2 - [AMA with Walicj.com](https://twitter.com/DecredCN/status/1245279133082324997) - Internet. DecredCN and Walicj.com jointly organized an AMA in WeChat group, mainly introducing Decred's governance model, atomic swaps, and dcrdex. The record was [posted](http://walicj.com/#/layout/article_detail/16720) on their site. (_missed in April_)
- Apr 23 - [Jueves CryptoDrinks Decred](https://twitter.com/Decred_ES/status/1253427311707213824) - Internet. [@elian](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158898257628136ERmQY:decred.org): "It was a very casual video call with community members of Blockchain Land and Decred was one of the hosts of the call. I gave a small brief on the project and the rest was answering questions about crypto in general (where to buy, how to store, how to spot scams, thoughts on the halving, strategies for trading, and if mining is profitable). It lasted for one hour and half and had 20-25 attendees." (_missed in April_)
- Apr 28 - [Panel on Cryptosecurity](https://twitter.com/elianhuesca/status/1255293877373800448) - Internet. [@elian](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158898257628136ERmQY:decred.org): "It was organised by Binance in Spanish and it was a sort of AMA but on crypto security, the questions were around how to store and OPSEC best practices. I got several opportunities to highlight Decred's work on hybrid blockchains, DEX, open source software, and hard fork resistance. There was a very good response from both the audience and the other guests of the AMA." (_missed in April_)
- May 2 - [Bitconf Live](https://www.eventbrite.com.br/e/bitconf-live-edition-tickets-103094542552) - Internet. Decred was a sponsor. Edilson Osorio Jr, creator, and CEO of OriginalMy gave a talk "The impact of blockchain during the pandemic" and introduced a [new app](https://devpost.com/software/open-prescription) to authenticate and validate the process of prescribing drugs without physical contact with the patient (Decred is one of the 4 blockchains used by the app). João Ferreira (@girino) talked about "Decentralization and Governance", DEX, atomic swaps, and Politeia, and this talk was watched by [~2,500](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158859699024140OzoCg:decred.org) people. The videos are available on [Facebook](https://www.bitconf.com.br/portal/2020/05/03/assista-as-palestras-da-bitconf-live-edition/) and [Decred Brasil](https://www.youtube.com/channel/UC73wa2ddXuPWsmenVfeFTYg) YouTube channel.
- May 6 - [Crypto Resources Livestream](https://twitter.com/cryptorc_tech/status/1257765517626130433) - Internet. The stream was 2 hours long and was watched by ~300 people. @camilolwi introduced blockchains and Bitcoin, and then @elian talked about Decred for almost an hour. ([video](https://www.youtube.com/watch?v=x2QUGV4ezZQ))
- May 7 - [Hablemos Decred 5](https://twitter.com/Decred_ES/status/1257774155677630464) - Internet. On the fifth edition of \#HablemosDecred the Latam team talked about cryptocurrencies and journalism with [Fernando Quiros](https://twitter.com/ferquiros_com) from [Cointelegraph in Spanish](https://twitter.com/EsCointelegraph).
- May 12 - [Consensus: Distributed](https://www.coindesk.com/events/consensus-2020) - Internet. Decred was represented by talks from @lukebp on Politeia, @matheusd on LN, @chappjc and @buck54321 on dcrdex and dcrdata, @Checkmate on on-chain insights, and finally @jy-p with an overview of 1 year of Decred development. All links in the [Media](#media) section below.
- May 13 - [Digital Governance](https://twitter.com/Decred_ES/status/1260574384667983875) - Internet. This ~20 person webinar about Decred, blockchain governance and decentralized digital currencies was co-organized with [Hack por la Paz](https://www.facebook.com/HackporlaPaz/). Questions revolved around understanding governance in our everyday lives, how that can be extrapolated to digital currencies and wealth, and the impact of CBDCs on the cryptocurrency markets. ([video](https://www.facebook.com/HackporlaPaz/videos/900552810355885/))
- May 14 - [Decentralized Governance Panel](https://twitter.com/Decred_ES/status/1258905004510973953) - Internet. @caibarrad and @adcade represented Decred in the panel "What is decentralized governance and DAOs?", which was co-organized with BlockchainEx and was part of the development of Decred ecosystem in Colombia. ([video](https://www.youtube.com/watch?v=Pvqp_1skrxM))
- May 16 - [Open-Source Funding Webinar](https://twitter.com/Decred_ES/status/1259984598102093828) - Internet. @victorarubin and @tomee co-organized the event with Hack Space Peru as part of outreach in the region. @pablito gave a presentation about one of the biggest challenges of open-source software, funding, explored more than a dozen approaches, and finally introduced the Decred solution. ([video](https://www.youtube.com/watch?v=UVtOBAAerXk))
- May 19 - [Latoken Blockchain Economic Forum](https://latoken.com/events/Keynote-133) - Internet. @elian gave a 36-minute keynote about Decred, project funding/expenditure, Politeia, LN, and the privacy implementation. ([video](https://www.youtube.com/watch?v=xZvp0us44wo))
- May 20 - Bitcoin and Crypto Panel - Internet. [@elian](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$159001320735424sZqPg:decred.org): "I was on a panel on Bitcoin and cryptocurrency use cases as part of Business Land at Talent Land, and highlighted Politeia and dcrtime as FOSS infrastructure with cases for government and enterprises, and how the DAO pays its global workforce. Also talked about the remittance market for DCR and payment processing infrastructure for increasing adoption." ([video](https://www.youtube.com/watch?v=gmWSmxb5yvg))
- May 25 - [BlockConf Digital](https://blockconf.digital/) - Internet. Decred was a [bronze sponsor](https://twitter.com/BlockconfD/status/1251194332079697922). Contrary to what was expected, it was not possible to know if people attended the virtual booth and there was no easy way to interact with people. @elian gave a talk on cryptocurrencies in Latam and a brief on Decred, Politeia, and the Latam proposal.

## Media

Selected articles:

- Decred on-chain: Mining pulse by @PermabullNino ([medium](https://medium.com/@permabullnino/decred-on-chain-mining-pulse-3b28d5155a04))
- Decred price: A seasonality study by OneAnalyst ([medium](https://medium.com/coinmonks/decred-price-a-seasonality-study-414bac98bc99))
- In the network - Decred by Lewis Harland ([formalverification.substack.com](https://formalverification.substack.com/p/in-the-network-decred))
- A more private way to stake by @jholdstock ([blog.decred.org](https://blog.decred.org/2020/06/02/A-More-Private-Way-to-Stake/))
- Decred. Forks in the road by @mrbulb ([github](https://github.com/monsieurbulb/forksintheroad/blob/master/Decred_forks_in_the_road.md))
- Four points of failure by Phoenix Green ([medium](https://medium.com/@Phoenixgreen/four-points-of-failure-2b1b2199397b))

Translations:

- A new kind of DEX - [in Spanish](https://medium.com/decred-es/un-nuevo-tipo-de-dex-8d7b5f8681c9) by @francov\_
- Politeia Digest 31 - [in Spanish](https://medium.com/decred-es/politeia-digest-edici%C3%B3n-31-abril-16-mayo-22-2020-28fc2fc75784) by @pablito. Congrats on the first PD translation!
- Decred Journal April 2020 was translated to Arabic (@arij), Chinese (@Dominic), Polish (@kozel), and Spanish (@francov\_). Notably, all four are on GitHub. Thank you all!

Videos:

- Decred bi-weekly news update - May 3rd, 2020 by @Exitus ([youtube](https://www.youtube.com/watch?v=oHqzvN3TMU0))
- Decred Construct feat. devs Luke Powell on Politeia & Matheus Degiovani on LN - Consensus 2020 ([youtube](https://www.youtube.com/watch?v=HexsUmqA7-Y))
- Decred Construct DEX interview feat. devs Brian Stafford and Jon Chappelow - Consensus 2020 ([youtube](https://www.youtube.com/watch?v=fS9j7RaawjY))
- Trade Secrets feat. Decred on-chain analyst Checkmate - Consensus 2020 ([youtube](https://www.youtube.com/watch?v=NOyyAx6Ab_0)) - @Checkmate talking about HODL conviction signals, realized price and MVRV, 142-day sum of USD ticket value, block subsidy valuation, transaction demand, and Treasury flows
- Decred Changelog overview feat. project lead Jake Yocom-Piatt - Consensus 2020 ([youtube](https://www.youtube.com/watch?v=OmwI62HZerg)) with Q&A ([youtube](https://www.youtube.com/watch?v=Uzf2ZGXWoss))
- 365 Decred days - CoinDesk ([coindesk.com](https://www.coindesk.com/video/365-decred-days)) - this is the full Decred Foundations program from the CoinDesk website, they broadcast it through Zoom so the quality is not as good as the YouTube uploads above
- Bull case for Decred, on chain metrics & monetary premiums with Checkmatey by Nugget's News ([youtube](https://www.youtube.com/watch?v=QWfq1tn8xs0))
- Akin Sawyerr joins @JillMalandrino on @Nasdaq \#TradeTalks to discuss governance on the blockchain to build a fairer financial system for all ([youtube](https://www.youtube.com/watch?v=NW-pwO9PUG4))
- Finding value in cryptocurrencies - economic, social, environment by Phoenix Green ([youtube](https://www.youtube.com/watch?v=4fwMXos3u3A)) - first YouTube video by the author, which he followed with 6 more [videos](https://www.youtube.com/channel/UCZSFAqUMp8v58eEQl_bzWYg) explaining different ways of buying DCR
- Decred bi-Weekly news update - May 22nd, 2020 by @Exitus ([youtube](https://www.youtube.com/watch?v=9i56ly5SS6M))

Audio:

- Gold Goats N Guns Podcast Ep. 34 - @jy-p and the case for a return to sovereign money ([tomluongo.me](https://tomluongo.me/2020/05/19/podcast-episode-34-jake-yocom-piatt-and-the-case-for-a-return-to-sovereign-money/))
- Decred in Depth Ep. 24 - @chappjc and @buck54321 talk about dcrdex ([libsyn](https://decredindepth.libsyn.com/chappj-buck-the-decred-dex))
- Decred in Depth Ep. 25 - @raedah talks about years working on Decred, from contributing to DCP-0001 and dcrdata, to newer projects like mobile wallets, forming a group with African and Asian devs, and the new Planet Decred proposal ([libsyn](https://decredindepth.libsyn.com/raedah-planet-decred-development), [soundcloud](https://soundcloud.com/decredindepth/raedah-planet-decred-dcr))
- Rough Consensus Ep. 5 - Deflation, dollars, & Decred. @mr.black, @Checkmate, and @PermabullNino discuss Bitcoin halving, the relief rally in traditional markets, the realities of deflation and inflation on the economy, and how Decred stands out as an undervalued SoV contender. ([libsyn](https://roughconsensus.libsyn.com/episode-5-deflation-dollars-decred))
- Rough Consensus Ep. 6 - Narratives with Seth Simmons. Seth joins the spidey crew to talk about how narratives drive the cryptocurrency space. ([libsyn](https://roughconsensus.libsyn.com/episode-6-narratives-with-seth-simmons))

## Community Discussions

Comm systems news:

- Riot released a [huge update](https://blog.riot.im/e2e-encryption-by-default-cross-signing-is-here/) which was deployed to chat.decred.org. End-to-end encryption is enabled by default for new DMs. Make sure to backup your keys to not lose access to encrypted chat history.

Selected Reddit posts:

- @mrbulb's [post](https://www.reddit.com/r/decred/comments/gnfjci/decred_forks_in_the_road/) about his "Forks in the road" article had 19 comments, mostly from people saying they appreciated it, but there is one user who has deleted their comments
- a commercial lawyer is really [impressed](https://www.reddit.com/r/decred/comments/gqewwe/really_impressed_by_decred/) by Decred
- pre-proposal for outreach in [Iran](https://www.reddit.com/r/decred/comments/glzckw/preproposal_decredforiran/)
- possible applications of [time locks](https://www.reddit.com/r/decred/comments/gcyquz/decred_timelocks/)

Selected Twitter discussions:

- on the day of Bitcoin halving, @ammarooni [reminds](https://twitter.com/Ammarooni/status/1259985075460063232) that Austrian economics recommends against abrupt changes to monetary issuance
- @lukebp getting more vocal on Twitter about [Politeia work](https://twitter.com/lukebp_/status/1258139602516193280)
- @lukebp [explains](https://twitter.com/lukebp_/status/1262871839035977728) Politeia, CMS and the DCC process in few short tweets
- @lukebp's translation of @moo31337 console output [to English](https://twitter.com/lukebp_/status/1263213648471707648) received an unusual amount of likes and replies discussing the mechanics of voting on Treasury transactions
- @chappjc makes the dcrdex testnet pre-alpha [official](https://twitter.com/chappjc/status/1267115398610255874)
- updated DCR market [charts](https://twitter.com/BlockCommons/status/1265379141995712512) following the end of MM activity, from @richardred
- @elian unveiled the [harsh reality](https://twitter.com/elianhuesca/status/1263463096401747970) about what is coming for bank accounts

> I gave my young son some Bitcoin at Christmas and was fearful he wouldn't engage and he hadn't mentioned it much since. Last week he came to me and asked "Should we not be stacking Decred Dad?" Ultimate Father/Son moment. ([@veganreboot](https://twitter.com/veganreboot/status/1265952035280732160))

## Markets

In May DCR was trading between USD 12.62-15.66 / BTC 0.0014-0.00167. The average daily rate was $14.11.

A [seasonality study](https://medium.com/coinmonks/decred-price-a-seasonality-study-414bac98bc99) by OneAnalyst explored day-of-the-week and month-of-the-year effect on DCR's daily returns (DCR seems to favor Saturdays).

A [wrap-up](https://blockcommons.red/publication/mm-phase1-wrapup/) of phase 1 market maker activity by @richardred analyzed order book depth over time for DCR and other assets, concluding that it didn't see an organic increase beyond the orders maintained by i2.

## Relevant External

Bitcoin's long-anticipated third halving of new issuance occurred on May 11, dominating the crypto news agenda for some period around this date and even penetrating [more](https://www.cnbc.com/2020/05/11/bitcoin-halving-heres-what-you-need-to-know.html) [mainstream](https://www.bbc.co.uk/news/business-52628034) [sources](https://www.independent.co.uk/life-style/gadgets-and-tech/features/bitcoin-halving-price-prediction-2020-a9488506.html) - much of it focusing on what effect it might have on the price.

One of several live events to mark the occasion, a seven-hour livestream organized by Cointelegraph, was unceremoniously [halted](https://cointelegraph.com/news/youtube-cancels-cointelegraphs-btc-halving-livestream-for-being-harmful-content) mid-stream and deleted by YouTube for being "harmful content".

The Dash Investment Foundation has responded to some friction (rejected proposals and private criticism from master nodes) by [announcing](https://github.com/DashInvests/dif-communication/blob/master/DIF_Statement_15.05.2020-For_Immediate_Release.pdf) that it will no longer seek decision-making autonomy and will reduce its ask from the Dash Treasury, coming up with a new VC strategy during Q2 2020.

Reddit introduced new blockchain-based tokens to be trialled on /r/cryptocurrency ([Moons](https://www.reddit.com/r/CryptoCurrency/comments/gj96lb/introducing_rcryptocurrency_moons/)) and /r/FortNiteBR ([Bricks](https://www.reddit.com/r/FortNiteBR/comments/gj8tm1/introducing_rfortnitebr_bricks/)). Tokens will be awarded to users of a subreddit in relation to their karma scores (50%), 10% for moderators, 20% for Reddit, and 20% for the "broader Reddit community". In addition to serving as a badge of reputation on the subreddit points can be used to unlock features like posting gifs in comments. Points-weighted variants of polls have also been described.

Tech giants and dozens of governments have decided that smartphones are not backdoored _enough_ and initiated an unprecedented mass [surveillance](https://en.wikipedia.org/wiki/COVID-19_surveillance#Digital_surveillance) program (attributed to COVID-19). Many [technologies](https://en.wikipedia.org/wiki/COVID-19_apps) have "privacy-preserving" added somewhere in the title and it might be [really secure](https://en.wikipedia.org/wiki/List_of_data_breaches) this time. There is even a promise to [terminate](https://www.cnet.com/news/apple-and-google-say-they-will-shut-down-covid-19-tracking-tools-once-pandemic-ends/) the tracking systems once the pandemic "ends". Sarcasm aside, for cryptocurrency users it means a bunch of new privacy and security risks on their mobile devices and a strong incentive to consider [alternative](https://itsfoss.com/open-source-alternatives-android/) operating systems or even hardware.

## About This Issue

This is issue 26 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, chappjc, degeri, elian, Exitus, l1ndseymm, richardred
- reviews and feedback: davecgh, dnldd, Dominic, emiliomann, jholdstock, jrick, lukebp, matheusd, raedah
- title image: saender
