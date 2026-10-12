# PRD & Prototype Sprint (Module 4)

## Pick & scope with MoSCoW
- **The “Now” feature I’m scoping (name + one-line core description):** Wallet - Ready Instant Card-Adds the card to Apple Pay and Google Pay on approval, before the physical card arrives
- **My finalized Must-Haves (after overriding the AI):** Instant virtual card issuance on approval. Paymentology issues a Mastercard virtual card the moment approval fires. Without it, she has no card to add.
Apple Pay provisioning with one tap. An in-app "Add to Apple Pay" button on the approval screen, using push provisioning and Mastercard tokenisation. This is the only way Riverty reaches her at the till. Apple Pay is the most used mobile method at German points of sale (Bundesbank).
Live for use at once. The card works for contactless and online payments straight after provisioning, with no waiting for the physical card or an activation step. "Before the physical card arrives" is the whole feature.
Card details for online checkout. The app shows the number, expiry and CVC behind biometric authentication. Many German online checkouts only take card numbers, and her friction is also "depends on whether Riverty is listed".
Strong customer authentication at provisioning. This is an enabling Must required for PSD2 compliance, and the feature cannot ship without it.
Real-time authorisation with basic fraud rules. This is an enabling Must from Risk, and a wallet card without it is unsafe to launch.
Suspend card or wallet token. Users can freeze the card if they lose the phone. This is an enabling Must for safety.
Failure state with retry and a support link. If provisioning fails, she sees a clear error, can retry, and can reach support. Without it she gets stuck at the moment she is most willing to adopt.
Event logging for the primary metric. Log the provisioning funnel and every card transaction with in-store or online flags. Without it the 90-day decision can't be made.
One approved wallet card art asset. It is typically required for wallet listing (confirm with Apple and Google). Use a single static design.
- **What I demoted from Must → Should/Won’t, and why:** should:
Google Pay provisioning. I deliberately narrowed the feature to Apple Pay first. Promote Google Pay to Must if the pilot cohort is more than about 30% Android. Check the cohort's device mix before sprint planning.
Real-time push notification per payment, showing merchant and amount, which helps with "later can't recall what I paid".
A short "how to pay in store" screen with the hold-your-phone-to-the-terminal gesture.
Partner-merchant guardrail instrumentation. This isn't needed for sprint 1, but it must be ready before the 90-day read.
Denominator for payment share. The primary metric needs her total monthly payments, and Riverty can't see Klarna, PayPal or bank spend. Start with a monthly in-app question.
could:
Apple Watch and Wear OS support.
Multi-device and token management screen.
Provisioning from an SMS or email deep link.
Custom or seasonal card art.
Samsung Wallet.
Merchant logos on transaction entries.
Open-banking aggregation of other providers' spend, as a better way to measure the denominator.
wont:
Default-card nudge, which is C3.
Cross-provider payment overview, which is C2.
Split It Later and instalments in wallet, which are C4. Apple's pay-later wallet slot (C9) stays blocked by CCD2.
Cashback or rewards, which is C7.
Credit limit and auto-repay changes, which is C8. Any new pricing, credit policy or terms change triggers a new regulatory approval.
Partner merchant perks, which is C6.
Changes to physical card fulfilment.
Any market outside Germany.

## Generate your Simplified PRD
- **One thing my PRD makes explicit that a vague brief would have missed:** It makes explicit that success is the card’s share of her monthly payments (14% to about 20%), not sign-ups, and it pairs that with a guardrail on partner-merchant GMV. A vague brief would say “increase card usage”. That could look like a win while moving purchases from Riverty’s roughly 2.9% merchant fee to about 0.3% interchange, and in my synthetic worst case that loses about EUR 11 per card a year.

## Prompt-to-prototype sprint
- **Where did the prototype reveal a gap in my PRD logic? (what I had to update):** “Try again keeps progress.” The PRD never said what that means. I made it skip the identity step and go straight back to adding the card.
The 3-tap target. The PRD counts “add, confirm, done”, but “done” isn’t a tap, because success appears automatically. The happy path is 2 taps.
Lockout scope. Three failed Face ID attempts lock the flow, but the PRD said nothing about failed Face ID when revealing card details. I made that a separate check that doesn’t lock.
Offline timing. The PRD didn’t say at which step “offline” is detected. I detect it after the identity check, when adding the card.
Testing edge cases. None of the failure paths could be tested without real Apple and Paymentology access. I added a scenario panel (not in the PRD) so a tester can trigger each one.
Must list versus prototype. Several Musts (real-time authorisation, fraud rules, wallet card art) can’t be prototyped. The PRD should mark which Musts are in scope for the prototype.
The “how to pay in store” hint. It is a Should item in the MoSCoW list, but the PRD puts it on the success screen. I kept it as lightweight text.
- **My prototype, as a link or a screenshot (publish or share from your tool; in Lovable that is Share → Share Preview, in Bolt Publish → Web. No share URL? Screenshot the working flow):** Riverty Wallet-Ready Instant Card_ prototype.html
