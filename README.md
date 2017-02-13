# aws-mfa
simple tool to deal with MFA when using AWS CLI

this tool will request session token using `aws-mfa` profile and override the `default`
profile with the result of the session token request

## How to use
- first you must have `~/.aws/credentials` (run `aws configure` to configure it)
- copy the `default` section to `aws-mfa`
- add `mfa_serial` option, it contain arn to your MFA device
- so your `~/.aws/credentials` will look like this
```
[default]
aws_access_key_id = AKIAI6WNGD275xxxxxxx
aws_secret_access_key = I+ij+NkPxxxxHXSWH/3bJxxxxc8xV2h2lxxxx

[aws-mfa]
aws_access_key_id = AKIAI6WNGD275xxxxxxx
aws_secret_access_key = I+ij+NkPxxxxHXSWH/3bJxxxxc8xV2h2lxxxx
mfa_serial = arn:aws:iam::3227270xxxxx:mfa/win
```
- run `aws-mfa <token>`, token is what you got from your MFA device
- it will rewrite your `~/.aws/credentials` to something like this:
```
[default]
aws_access_key_id = ASIAIEUEAGTBJRIxxxxx
aws_secret_access_key = 4oDfkeZ2d1n+zbY1xxxxxEXLMIO7YxrYxxxxx
aws_session_token = FQoDYXdzENP//////////wEaDP3t7VMse3xxxxxxxAYeRE85mYWSfYA06zsbF4/gLJ0xdFhQRkxxxxxxxxFys3ZGR83FAlg02l0htrXrHG29MIUJBlynuwffxpwzaeKjaJX5b/qo37HnPMjlN/itI10JN6TTQ6nOQgeHdGytM7fdCplwCXPCq88a55sB66D0rhGPZvTEohYd5wmCdMuHz/5F51PPJZ/qTBNKvIQb/ejThC2b49HGQIJ3YqK/pDKoGrNmCUNwNFKKCOhsUF

[aws-mfa]
aws_access_key_id = AKIAI6WNGD275xxxxxxx
aws_secret_access_key = I+ij+NkPxxxxHXSWH/3bJxxxxc8xV2h2lxxxx
mfa_serial = arn:aws:iam::3227270xxxxx:mfa/win
```


NOTE:
- you need to run `aws-mfa <token>` again when the `default` credential is expired
