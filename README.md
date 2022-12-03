# Valuation Rate Curve Bootstrapping

Valuation rate curves are foundations for FX derivative products because the rate curves serve two main purposes: the single curve can be used to discount future cash flows; and the pair curves can be used to estimate FX forward rates.

The proposed USD curve has three key instruments: Cash rate (short term up to 3 months), 3-month Futures (medium term), and 3 month swaps (long term up to 5 years). This proposed curve follows market practices.

The Revaluation Rate Curve is used for two purposes: the first is being used to construct US dollar interest rate curve; while the second is used to derive the other currencies interest rate curves based on the US dollar curve.

The model’s input components are: market quotes of underlying instruments, all parameter settings including business convention, day count, interpolation method, etc.

The key assumptions are
•	Market-quoted underlying instruments are sufficiently liquid to reflect their real market value.
•	Linear interpolation on rates method used in the US dollar interest rate curve construction process assumes that rates implied from the curve follow linear relationship. 
•	No arbitrage
•	No counterparty default risk

There are two steps in the procedure.
•	First, convert the US dollar interest rate curve from market quotes into zero swap rates and discount factors.
•	Second, derive the other currencies’ interest rate curve based on the base currency (US dollar) interest rate curve, spot FX rate, and the swap rate.

To derive discount factors and zero swap rates from the US dollar market quoted interest rate curve, the underlying instruments can be deposit rates (Rd), futures (Rf), or swap rates (Rs). It is straightforward to derive zero swap rates (Rz) and discount factors from the deposit rates and futures:

 

where t2 > t1 > t0, base is the year convention.

For a swap rate, an assumption on interpolation method is needed. The setting used is linear interpolation on rates:

 

After the zero swap rate is known, it is easily converted to the discount factor using the following formula:

 

This approach is usually referred to as interest rate parity. This process assumes no arbitrage. That is, the returns from borrowing in one currency, exchanging that currency for another currency, and investing in the second currency while simultaneously purchasing futures to convert the currency back at the end of the holding period should be equal to the returns from purchasing and holding the first currency investment. If the returns are different, an arbitrage transaction could produce free money.

 

where S(t0, t1) is the spot forward, t1 = t0 + 2 for most FX pairs, FR(t1, t2) is the outright forward, capfd(t1, t2) is the capital factor for the domestic currency and capff(t1, t2) is the capital factor for the foreign currency.

The FX swap combines a spot deal and a forward contract. The difference (Forward rate– Spot)*factor is called the forward points or FX swap rate. If the exchange rate is quoted to four decimal places, the factor is set as 10,000; if the rate is quoted to two decimal places, the factor is 100. SR(t1, t2) is the swap rate coming from the market-quoted forward points.

From the above formulas, given the base currency’s discount factor, FX spot forward and forward points, one can back out another currency’s discount factor (ref https://finpricing.com/lib/EqCallable.html).
