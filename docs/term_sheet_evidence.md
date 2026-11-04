# Term sheet evidence (public SEC filings)

Real margin loan and equity swap terms found in SEC EDGAR exhibits, used to calibrate the loan and TRS simulation. All documents are public filings.

## Margin loans

| Deal | Year | Ladder (LTV) | Cure | Other triggers | Rate | Source |
| --- | --- | --- | --- | --- | --- | --- |
| Musk / Tesla shares (Twitter financing), Morgan Stanley lead, 11 banks | 2022 | Max initial 20%, call 35%, cure to reset 25%, release 15% | 2 business days, back to the reset level | Mandatory prepayment if VWAP < 40% of the closing price on the funding date | 3m Term SOFR (floor 0) + 3.00% | [EX-99.D, SC 13D/A](https://www.sec.gov/Archives/edgar/data/1418091/000110465922048128/tm2213229d1_ex99-d.htm) |
| HNA / Hilton, Park, HGV shares | 2017 | In fee letter (not public); prepayment targets 37.5% and 32% LTV; release test LTV <= 40% for 10 days | 2 scheduled trading days after the call notice; prepayment in steps of 25% / 25% / 50% on days 2, 3 and 5 | 1-day collateral value drop >= 15%, 4-day drop >= 25%; 40-day ADTV < 50% of reference cuts the collateral value to 80% | n/a | [EX-99.B, SC 13D/A](https://www.sec.gov/Archives/edgar/data/1585689/000119312517383682/d517534dex99b.htm) |
| Icahn / Navistar | 2015 | Collateral Shares Trigger: collateral value <= 45% of its closing-date value | n/a | n/a | n/a | [EX-99.2, SC 13D/A](https://www.sec.gov/Archives/edgar/data/808450/000119312515028010/d855166dex992.htm) |
| Others to review | | Verint (Apax), TransAlta (Brookfield), Sina (Charles Chao) | | | | EDGAR full-text search |

## Equity total return swaps

| Deal | Year | Collateral | Price trigger | Equity notional reset | Floating leg | Source |
| --- | --- | --- | --- | --- | --- | --- |
| Pirelli / Olimpia, JPMorgan | 2002 | IA = EUR 0; CSA applies once a trigger is hit | Barrier EUR 0.875 vs initial EUR 1.4213 (61.6%): 3 consecutive closes below it is an Additional Termination Event unless collateral is posted | Not stated | 3m EURIBOR + 1.43%, Act/360 | [EX-99, SC 13D/A](https://www.sec.gov/Archives/edgar/data/1156964/000090951802000136/jpm.txt) |
| Seabridge Gold, National Bank of Canada | 2017 | IA = 100% of notional (fully collateralised) | None | Not applicable | LIBOR + 1.20% to 1.25% | [EX-99.18, SC 13D/A](https://www.sec.gov/Archives/edgar/data/1231346/000101905617000503/ex99_18.htm) |
| CoreLogic (Senator / Cannae) master confirmation | 2020 | IA per supplemental confirmation, under the CSA | None | Not applicable | USD LIBOR + spread (blank) | [EX-99.5, SC 13D/A](https://www.sec.gov/Archives/edgar/data/36047/000119312520212032/d46895dex995.htm) |
| VimpelCom ADR, ING | 2010 | n/a | None | Applicable | 1-week USD LIBOR + 1.10% | [EX-99.1, SC 13D/A](https://www.sec.gov/Archives/edgar/data/1468091/000095012310057427/u09106exv99w1.htm) |

## What this changes in the simulation (to decide)

1. Margin loans: cure back to a **reset level** between the opening and call levels (Musk: 20 / 25 / 35), not back to the opening LTV. Add a release level.
2. Margin loans: add a **share price event** (price below X% of the initial price) and **liquidity triggers** (ADTV falls versus a reference level); HNA shows banks write volatility and liquidity directly into the contract.
3. TRS: margin is an **Independent Amount** (0% to 100% of notional) plus daily variation margin under a CSA. The early-warning event is a **barrier**: N consecutive closes below X% of the initial price.
4. TRS: an equity notional reset was in 1 of 4 swaps. Make it a per-contract flag, not the default for the whole book.
5. Financing: reference rate + spread, observed 1.10% to 1.43% on TRS and 3.00% on the Musk loan. Set the spread and desk fee per contract.

Caveat: these are mostly US activist and acquisition financings disclosed under Schedule 13D, not European bank SET term sheets. Exact ladders often sit in fee letters that are not filed.
