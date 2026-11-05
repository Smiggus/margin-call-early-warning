# Deal universe: real share-backed financings

287 unique real deals (289 rows, 2 cross-source duplicates flagged) from three sweeps, used to calibrate the simulated book and to build a real-deal test set. The CSV (`deal_universe.csv`) is data and stays out of Git: store it with the raw data, not in the repo.

| Source set | Rows | What it adds |
| --- | --- | --- |
| SEC EDGAR (13D Item 6, Form 4 footnotes) | 192 | Sponsor margin loans with lender, amount and shares pledged; forced sales with date, shares and price |
| European disclosures and cases (AMF, Companies House, BaFin, CNMV, courts, press) | 60 | Bollore/Vivendi, Adler/Vonovia, Sacyr/Repsol, Wirecard/Braun, Schaeffler, Porsche/VW, Altice/BT, Frasers/Ashley |
| Court cases and academic sources | 37 (35 unique) | Archegos (7 banks), Luckin, Tellurian/Souki, Layne v. Bank One, Valeant/Pearson, McClendon, Musk |

Earlier term-sheet evidence: `term_sheet_evidence.md`, `term_sheet_evidence_round2.md`.

## Coverage

- Product: margin loan 161, share pledge 71, prepaid forward 25, TRS 14, collar 12, other 4.
- Outcome: forced sale 95, foreclosed 29, defaulted 10, cured 7, called 3 (144 distress outcomes); prepaid 24, none known 113, unknown 6.
- Period (origination or outcome year, 284 dated): 1998-2005: 25, 2006-10: 80, 2011-15: 39, 2016-20: 60, 2021-26: 80.
- Terms: 51 deals carry at least one numeric term; 19 carry an initial LTV (implied median 0.34, range 0.15 to 0.93).

## Calibration points

- Initial LTV: about 20% to 50% in most deals (Musk 20%, Altice/BT 60% stated, Bollore about 70% implied).
- Call frequency: 15% of US CEOs with margin loans faced margin-call-driven selling, 2007-2016; average pledge 38% of holdings (court and academic notes).
- Cure: 1 to 5 business days in US and European deals; 2 days is the mode (Musk, HNA, Adler/Vonovia, Extended Stay).
- Persistence: 3 consecutive closes below the trigger (Sacyr/Repsol EUR 12.48, Pirelli/JPM barrier).
- Liquidation: pledged shares sold at 5% to 15% of daily volume (Tellurian/Souki, held commercially reasonable); about one week from call to sale (Valeant/Pearson).

## Caveats

- Call, reset and release levels, cure days and spreads are rarely disclosed in US deals after about 2015 (unfiled side letters).
- Outcome labels are the researchers' reading of the events; read each row's `outcome_note` before using one as a target.
- Lender names tagged `inf` are inferred. Where no agreement date is given, `origination_date` is the filing date.
- The Form 4 sweep had a few failed search windows, so forced-sale coverage is incomplete.
- Evidence tags: `doc` primary document, `inf` inference or arithmetic, `red` redacted in the document, `press` press or secondary summary.
- Spot checks: 3 random EDGAR rows matched their filings (Centennial repayment, Sterling Construction margin-call sale, Alkami / General Atlantic pledge).
