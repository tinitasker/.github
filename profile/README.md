# TiniTasker API
TiniTasker is a digital platform designed for the Canadian service businesses specific needs.

## Business information
TiniTasker is a b2b saas. Product provides various of functionality that helps technicians and business owners with keeping the data clear and ordered.

## Technical details
The platform is represented as combination of public/internal APIs and public clients (mobile app, web portal and web public).

#### APIs
APIs are written in `C# / ASP.NET Core` using service-oriented architecture.
- [API](https://github.com/tinitasker/api) - The main product API
- [Identity](https://github.com/tinitasker/identity) - The self-written OIDC provider
- [Storage](https://github.com/tinitasker/storage) - The wrapper on DigitalOcean Spaces (S3-compatible file storage)
- [Messaging](https://github.com/tinitasker/messaging) - The wrapper on notifications (Resend/FCM)

#### Hosting
The platform is hosted on [DigitalOcean](https://cloud.digitalocean.com) using managed infrastructure components in Toronto region datacenter/-s.

#### Front-end
The platform provides 3 public applications:
- [Mobile app](https://github.com/tinitasker/app) - Mobile app for business owners / technicians
- [Web portal](https://github.com/tinitasker/web-portal) - Internal web dashboard for business owners / maangers
- [Web public](https://github.com/tinitasker/web-public) - Public marketing website

## Canadian Taxes and Timezones
#### Tax rates in Canada (as of 2026)
- `GST` - Goods and Services Tax
    - A federal tax of `5%` applied across all provinces and territories.
- `HST` - Harmonized Sales Tax
    - A single, combined tax - federal + provincial in participating provinces.
- `PST/QST/RST` - Provincial Sales Tax / Quebec Sales Tax / Retail Sales Tax
    - A provincial tax added on top of the `5%` GST.

#### Canadian sales tax structure by province (as of 2026)
| Province                | Tax type  | GST (%) | HST (%) | PST (%) | QST (%) | Total tax (%) |
|-------------------------|-----------|---------|---------|---------|---------|---------------|
| Alberta                 | GST       | 5       | N/A     | N/A     | N/A     | 5             |
| British Columbia        | GST + PST | 5       | N/A     | 7       | N/A     | 12            |
| Manitoba                | GST + PST | 5       | N/A     | 7       | N/A     | 12            |
| New Brunswick           | HST       | N/A     | 15      | N/A     | N/A     | 15            |
| Newfoundland & Labrador | HST       | N/A     | 15      | N/A     | N/A     | 15            |
| Northwest Territories   | GST       | 5       | N/A     | N/A     | N/A     | 5             |
| Nova Scotia             | HST       | N/A     | 15      | N/A     | N/A     | 15            |
| Nunavut                 | GST       | 5       | N/A     | N/A     | N/A     | 5             |
| Ontario                 | HST       | N/A     | 13      | N/A     | N/A     | 13            |
| Prince Edward Island    | HST       | N/A     | 15      | N/A     | N/A     | 15            |
| Quebec                  | GST + QST | 5       | N/A     | N/A     | 9.975   | 14.975        |
| Saskatchewan            | GST + PST | 5       | N/A     | 6       | N/A     | 11            |
| Yukon                   | GST       | 5       | N/A     | N/A     | N/A     | 5             |

#### Note on TiniTasker and Canadian Taxes
In TiniTasker, we primarily deal with `GST` and `PST`. `HST` is not directly represented but can be calculated based on the province's `GST` and `PST` rates.

- **GST** - `GST/HST` - represents either `GST` or `HST` depending on the province.
- **PST** - `PST/QST` - represents the provincial portion of the tax where applicable.

#### Canadian timezones
| Timezone            | Abbreviation | UTC Offset |
|---------------------|--------------|------------|
| Canada/Newfoundland | NST          | UTC-3:30   |
| Canada/Atlantic     | AST          | UTC-4      |
| Canada/Eastern      | EST          | UTC-5      |
| Canada/Central      | CST          | UTC-6      |
| Canada/Mountain     | MST          | UTC-7      |
| Canada/Pacific      | PST          | UTC-8      |
