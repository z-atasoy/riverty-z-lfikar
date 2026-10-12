# A/B Experiment Brief, Riverty business-unit case

## Parameters
| Parameter | Decision |
|---|---|
| Feature under test | C1 Wallet-Ready Instant Card. On approval, Paymentology issues a virtual Mastercard, and one tap adds it to Apple Pay after a strong customer authentication check. It works for contactless and online payments at once, with no activation step. Card details sit behind biometric confirmation. The card can be frozen, a failed add shows a reason, retry and support link, and every step is logged. Out of scope: Google Pay, nudges, instalments, rewards, and any change to pricing, credit or terms. |
| Persona | Nadine, 38, a frequent online shopper who uses 3 or more payment methods a month. She wants one consistent way to pay, online and in store, with fewer decisions. Her moment of misery is standing at a till or checkout and having to remember which method works where. |
| Expected outcome | The card becomes her default way to pay, and its share of her monthly payments rises from 14% to at least 18% over days 61–90 after activation. |
| Primary success metric | The card’s share of an active cardholder’s monthly payments (card payments ÷ all her payments in the month). Card payments come from the event log, and her total payments come from a monthly in-app question. |
| Baseline rate | 14%, from the friends-and-family pilot (synthetic). It rests on 69 activated users, so re-measure it in the canary week. |
| Guardrail metric | Riverty checkout GMV at partner merchants per cardholder, treatment vs control. |
| Guardrail boundary | Treatment must not be more than 5% below control over a rolling 28 days. If it is breached in 2 consecutive weekly reads, pause rollout. |
| Second guardrail | 30+ day arrears rate, with a 1.4% baseline and a 2.0% ceiling (monitoring trigger, not a significance test). |
| Minimum Detectable Effect | +4 percentage points absolute (14% → 18%) |
| Sample size per arm | 1.318 |
| Traffic split | 50 / 50 |
| Test duration | 22 weeks |
| Significance threshold | p < 0.05 |

## Control vs. Variant
- **Control (A):** At approval, Nadine sees “You’re approved” with the card art, and the line “Your physical card is on its way. You can add it to Apple Pay once it arrives.” Her virtual card is live for online use from approval, with card details behind biometric confirmation and a Freeze card toggle. Once the physical card arrives she can add it to Apple Pay through the same flow as B. Until then she can’t pay in a shop from her phone, so she falls back on whichever method she already carries. This is her moment of misery (M2): at a till or checkout she has to remember which method works where, and later may not recall whether she paid with Klarna, PayPal or her bank (UXR-11). The unchanged experience produces these numbers (M3, synthetic): 78% of users use 3 or more payment methods, Riverty is picked 6% of the time next to Klarna or PayPal, and 14% of cardholders’ monthly payments go through the card.
- **Variant (B):** The one change: Add to Apple Pay is offered at approval, instead of after the physical card arrives. Screens (from the M4 PRD):

Entry point, “You’re approved”: the card art, a one-line promise (“Pay with Riverty in any store, from your phone”), a primary Add to Apple Pay button and a Not now link.
Feature core, “Adding your card”: a confirm-it’s-you step, a progress state, and the failure state (reason, Try again, Contact support).
Success, “Your card is ready”: a Live in Apple Pay chip, a three-step in-store hint, Show card details and a Freeze card toggle.
- **Held constant (isolation check):** Identical in both arms, except for the Apple Pay offer on screen 1 and its timing:

The application, KYC, credit decision, approval criteria and population (Germany, iPhone users).
The same Mastercard card, pricing, credit policy and terms.
A virtual card live for online use from approval, with card details behind biometric confirmation.
Strong customer authentication, real-time authorisation, fraud rules and the Freeze control.
The wallet-add flow itself, which A also reaches, just later.
No nudges, push notifications, promotions or Google Pay.
Riverty checkout at partner merchants.
The same event definitions, payment-share definition and days 61–90 readout window.
The same app build, released to both arms at the same time.

## Hypothesis
> I believe that C1 Wallet-Ready Instant Card. On approval, Paymentology issues a virtual Mastercard, and one tap adds it to Apple Pay after a strong customer authentication check. It works for contactless and online payments at once, with no activation step. Card details sit behind biometric confirmation. The card can be frozen, a failed add shows a reason, retry and support link, and every step is logged. Out of scope: Google Pay, nudges, instalments, rewards, and any change to pricing, credit or terms. for Nadine, 38, a frequent online shopper who uses 3 or more payment methods a month. She wants one consistent way to pay, online and in store, with fewer decisions. Her moment of misery is standing at a till or checkout and having to remember which method works where. will result in The card becomes her default way to pay, and its share of her monthly payments rises from 14% to at least 18% over days 61–90 after activation., as measured by a +4 percentage points absolute (14% → 18%) change in The card’s share of an active cardholder’s monthly payments (card payments ÷ all her payments in the month). Card payments come from the event log, and her total payments come from a monthly in-app question. within 22 weeks. We will protect Riverty checkout GMV at partner merchants per cardholder, treatment vs control. throughout the test.

## Shipping criteria
> We will **ship** if The card’s share of an active cardholder’s monthly payments (card payments ÷ all her payments in the month). Card payments come from the event log, and her total payments come from a monthly in-app question. improves by ≥ +4 percentage points absolute (14% → 18%) at p < 0.05 and Riverty checkout GMV at partner merchants per cardholder, treatment vs control. does not reach Treatment must not be more than 5% below control over a rolling 28 days. If it is breached in 2 consecutive weekly reads, pause rollout. after 22 weeks.
> We will **iterate** if direction is positive but lift is below the MDE.
> We will **kill** if the primary metric shows no improvement or moves negatively.
> The read date is fixed at the end of 22 weeks, no results reviewed before this date.
