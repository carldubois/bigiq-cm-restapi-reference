Enable and enforce a specific signature in a policy by signatureId
------------------------------------------------------------------

Overview
~~~~~~~~

Describes how you use the REST API to update the attributes of a
specific signature in a policy.

Prerequisites
~~~~~~~~~~~~~

1. Retrieve a policy selfLink using the policy name, as shown on other
   examples in this chapter.
2. Find the signatureId that needs to be updated. The signatureId is
   shown on the BIG-IP and BIG-IQ UI and is reported in violation logs.
   ### Description Describes how you use the REST API to update the
   attributes of a specific signature in a policy. Perform the REST API
   actions in the following order:
3. Perform a GET operation to the signatures collection to retrieve a
   seflLink of a signature.
4. Perform a GET operation to the policy signatures to validate that the
   signature is listed within the security policy signatures.
5. Perform a POST operation with the new attributes to a special URI
   that updates policy signature attributes.

Description
~~~~~~~~~~~

The following extended example shows each of these REST API actions. ###
Example #### 1. Perform a GET operation to the signatures collection to
retrieve a seflLink of a signature. Perform a GET operation to the
signatures collection to retrieve a seflLink of a signature.

::

    GET: https://<mgmtip>/mgmt/cm/asm/working-config/signatures/$filter=signatureId eq '<signatureId>'?$select=signatureId,selfLink

The following is the JSON response from the GET operation:

::

    {
        "selfLink": "https://localhost/mgmt/cm/asm/working-config/signatures",
        "totalItems": 1,
        "items": [
            {
                "signatureId": "200010008",
                "selfLink": "https://localhost/mgmt/cm/asm/working-config/signatures/152bcf94-4ab3-3f8b-b524-4648f83249e0"
            }
        ],
        "generation": 2925,
        "kind": "cm:asm:working-config:signatures:signaturecollectionstate",
        "lastUpdateMicros": 1479385001323905
    }

2. Perform a GET operation to the policy signatures to validate that the signature is listed within the security policy signatures.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a GET operation on the signatures sub collection link, with a
special parameter called 'filterBySignatureSets' that limits the results
to signatures that are part of the sets that are defined in the policy.
The signatures sub collection link can be found in the
'signatureReference' reference structure (link attribute) in the policy
above. The link can also be determined by the policy selfLink - add
'/signatures' to the policy selfLink. The same logic applies to all
other sub collections as listed above. Note - further filtering by the
'enabled'/'performStaging' attributes cannot be done by the REST APIs.
Such filtering should be done by the caller with the retrieved results.
To validate that the signature is used in the policy, validate that the
'selfLink' obtained in step #1 is set in one of the signatures as the
value of the link attribute of the signatureReference structure.

::

    GET: https://<mgmtip>/mgmt/cm/asm/working-config/policies/<id>/signatures?filterBySignatureSets=true

The following is the JSON response from the GET operation:

::

    {
        "items": [
            {
                "signatures": [
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e00a9199-9644-33e8-af24-2c2dea6eb755"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"ancestor\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ee725e31-406e-3433-be96-22fe07ae9474"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( generic suntzu )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f76a79c2-8924-3a9c-b0bd-36ed9c1a6351"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "LDAP injection attempt ( objectcategory )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9c6d6072-511a-3e62-85ab-6cfc73faa75a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "c++ code leakage"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/63aee446-5a2a-3a8d-8c5d-abe949593f11"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_loginconfig"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d80d1e9b-eafc-35d1-957b-851964069d74"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"UPDATE SET WHERE\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b3a5e945-2c84-37c2-8fa1-f8f8456579b7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (9)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2b460f22-7408-3d70-8ae1-b007df22f4b2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "link href rel stylesheet (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2ddea994-5922-3cf5-a05b-981c85b76072"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url javascript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/31b7fcb2-59bb-3dce-965b-365e3f6c0439"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "background: url() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bdd12c4d-4d7f-3775-b1a5-51471694fda7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onredo (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f3a3f9e6-d1cd-3594-957f-0e6b8bf0dca3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url vbscript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/62fc54eb-8436-3b19-9266-ca280de28f6a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript buffer overflow attempt 3 (Response)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5f0bd68c-3b29-38da-8bd4-2d1e8df976bb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = application / x-shockwave-flash (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7cabd557-e1ca-387f-b4ab-8b154d5786d2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"fn:doc\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1ea6fd65-de5d-39a7-ba4b-8402202f35d7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"end-quote UNION\" (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/820d4c5f-75c2-3cfb-8cdf-7c943438eb43"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Padding Oracle attack (Padbuster)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/43c56023-46c1-3170-a5a7-57ca5238924b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onLoseCapture() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b6b3668b-3daa-3a32-bff9-7550ed414e69"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "#RefRef DoS tool (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b7c47b47-ad98-3ef8-bd9f-dc313b47569b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript buffer overflow attempt 1"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dddc2d8c-cb0f-3a54-ae07-abf6142f619f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT LOAD_FILE()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/30432b2c-bb60-35e7-88a3-0d7706019f39"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"isnull\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/837fee6a-8541-3cba-9b28-5d7262c3e9bb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XMLData. (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6b3a96b5-f02d-38e1-9872-1b662dd3c6cc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "param tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f89b5d94-3a93-3dea-95cf-940ef1b1cf84"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sys.user$ (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7942ea03-ea97-3236-a1a6-8c844906e215"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysconstraints (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/66427973-8a13-3b15-a828-7093c73e593b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ substr() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0249e525-dd5c-3313-a0c5-953d9c13571e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "input type image (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e937c891-5cf0-3c97-b535-1e5f4a469c34"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select instr"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a1c1d865-4400-319c-a89c-4c0ce78b9526"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"begin declare\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3fcf37cb-a93d-3f76-88e1-bb8977212689"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onFinish() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7eed7aa9-a6d7-3446-a573-8647339e9d38"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "confirm() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e7a35ef7-86f6-3262-9ae8-71e76a212263"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTML entity - &#x... (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/77ac10e7-13d3-362d-a120-c4894a79ec2a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"master..\" database (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9e1cb083-e318-37ff-aee0-18af132bbef2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTML entity - &#x... (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4161fe00-9817-3344-a38d-d95c1c48d407"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "video poster (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1490099f-9c9e-327b-a48e-d9ba68198a41"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onkeydown (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/05718d50-dfc9-371a-85d2-c807c78c25f9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"declare begin\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/861ae5e8-e24d-3cb9-a8e4-f4f7501bc06d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ 1,1,1"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cf60ab08-20be-3a96-8e5c-20c549e941aa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onContextMenu() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8f6b33d8-a610-3ccc-bb92-d3f5884ce321"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( .nasl )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/847234a1-ce39-33dd-a047-2d18a22fdadf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onhaschange (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6160915a-6bbf-3483-87d1-99556243f368"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "STYLE : behavior (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6afa241d-3a8b-3848-baf2-12531e229c2f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ insert into (2) (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/28f24dfe-df24-38c1-a6b1-02b0b818a34b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Injection: End Transaction (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c205c23b-e294-3280-a142-f524f6b8455c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XMLData. (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6a0730ea-a205-3c60-a596-9aaec4c008a3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Listing"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/944f04b4-2aad-3620-86c2-0b1c3e424340"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /.it/viewde )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/97e1cf3d-6ac5-3854-855a-41ad87cf0a1e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"Microsoft Office Protocol Discovery\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0c9aa298-5be8-3ad4-bb23-fdb54911dbef"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"DROP SCHEMA\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/af4e2333-43f5-31ef-a30a-be06a83ba847"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ user_group"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/edf3ca59-6c48-31ef-8244-9a1b508a2dca"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "decodeURIcomponent() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ce77e0bd-8398-35d6-bde2-840404cf3970"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onemptied (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/786edd7c-d59f-3d04-9c48-f762db89752b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( MyShell ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1b31f3a9-c214-34f0-b408-5d58b4fd2cd8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src shell (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1bc536c4-9951-3ee6-a479-73c61ba32672"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Injection: End Transaction (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a61265b8-e92e-3b34-871b-cc0166fd092e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "decodeURIcomponent() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d61e7b68-dba5-3358-b246-94b00c3fcbea"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onkeypress (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aca2ff8b-78c9-3b62-9558-a206a7b5f9f0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (bwh3_user_agent)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/21d60c7b-748f-3890-aedc-45db4505b5ca"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Session Fixation Attempt - 1 (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8f3bd653-36a8-3810-bc69-c496fc339fcb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onCopy() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/721b1290-2b52-393b-bb1f-72c3443042b1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"x-aaaaaa\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/04576d45-2aea-361c-91b6-9ba5faa5bcff"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "[document] (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/80d34f0e-591c-3872-8a97-62f5f2ffb452"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"load_file()\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9da735c0-0ef3-3f4f-93e6-c7144fbd77d6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \" and 1=1 (6) (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/75332db0-2cee-3631-91cd-69b8a8e29d74"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ bitand (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/05ad90a9-f885-3b1b-8576-6aa18c8ddde6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic XSS evasion (Headers) - unicode characters"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3c5b0214-691e-39a0-a47a-11e240416f7d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ integer field UNION (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/30307b77-6f1f-37aa-bead-21d570faf8bc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select ascii"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b38db25e-92cd-38c2-ab71-a70192519e51"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "OpenAsTextStream() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5ba6518b-1d8a-3b96-bab7-18c83e9d4b80"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href ecmascript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1b6458ee-0723-37d2-8b14-5281c3d9dec1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "execute() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/30e5fbc0-9d33-36b9-82f4-b1d2a2e194d8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (atSpider)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3576313c-0873-344d-a3ff-c75a8d51f48b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Pushdo botnet traffic - Probe request (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3ecc45e7-3963-3aba-bcc7-2077fdf4c305"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "/_admin access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2e0691b7-37b0-35c9-b8a9-59cb307f8caa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_regread"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/76a14053-8c3d-3702-9ec9-bc380f18cb72"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select data-type"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d6544dc6-281a-32ee-86a7-d610dda1129a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (WEP Search)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3d378cb7-c879-3285-a81b-21c9d612e48f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ waitfor delay (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/23315489-7e98-3fa3-bc3d-c83a63447b42"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (DBrowse)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d77fc3fd-52e8-37f0-9234-c87a781796e1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( scanalert )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/602fe29a-300c-390f-9881-a9a4f00807e8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"preg_\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a7b53412-b23a-3bea-943c-eb89bce04a33"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"microsoft url control\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/657bd2f5-951d-3c6c-be7d-992573ddad3e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "eval; (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0d860347-d77c-3a59-9f38-ed89a8d7b88e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"Missigua\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/50e879a7-c55d-35db-a06f-e19517e968ff"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CSSHttpRequest (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ac7355bf-a24e-3a35-a9b3-24a4af93bfc0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"webemailextrac\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c5ea5c54-6084-335f-a700-ffc7b1dd1c5b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"combine\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6508d6d-072b-34e5-9241-55fb56ea2dcf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"' and 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c878a12e-8b35-369d-b81d-b2cc01336b50"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onloadstart (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5142be5f-0f95-3f5e-afa3-836c578d677e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onPause() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/33b8038c-6ccd-3602-a4cc-9aed584c7589"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( Gamma Web Shell ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c6adfb22-78bb-3dc6-baa5-0e3caea951bc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTML comment (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fbb733a8-7229-3d0b-b349-fa11f4563140"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"CheeseBot\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e864d6cf-f31a-3319-92c5-d93b65b3bb00"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<MATH href (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/277d76aa-6a08-3ecf-bfff-663aed85a9d2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Falcove )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/987879dd-ad48-3990-b6f8-eedaa059fd8f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "touchstart (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/606fcbd6-4a40-3092-a88b-e4dfa343db5a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ user_ind_columns"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b6541813-a262-3be8-8a7c-c9a8d10c9d4f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "param tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a8d45f95-e3b7-3763-8799-56c7dcfc6449"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onwaiting (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6767660-4e8f-3c32-adf2-a21545c7d70a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"master..\" database (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1caa25fb-c8ea-3315-9d48-35cb97ccaf53"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onPaste() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/328dd269-2a3a-3f02-b996-78a46fc3facb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XMLHttpRequest() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/93341634-e87b-3098-99f6-bbd53d884583"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ImageMagick arbitrary file deletion (ephemeral)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7aa6632b-028c-3b88-899f-afbb04f344e2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "asfunction: (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0488da6f-7a06-3576-903d-becb233547bd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onkeydown (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d59a1b15-a360-3629-b4cf-7b2c5e828744"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url javascript (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fdcd9c72-6010-368a-949a-9ef3bc505c5c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "livescript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/268e4c04-b0f2-3e80-872a-2352d9812abd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "link href rel stylesheet (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/98bf3c90-9611-3740-b4ef-7e0c68621529"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".addimport (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8192ed03-159e-380d-86a1-e7e2dcfc90ef"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Session Fixation Attempt - 4 (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cecaf2be-e5c4-3873-a8a5-14d0fc806680"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop trigger"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4644ccd6-28e6-3d9b-b53f-2b97813e9edd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( News Remote PHP Shell Injection ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d7fc6818-94e7-3d40-ab76-02719dcb2ff9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"rsync\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2b1e9de3-9320-3694-9ead-81847550355b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( \"an exploit\" )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/20babba6-8cd3-3668-825a-57900747bb9c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style list-style-image:url (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3f0176fe-52ab-35b1-af23-c14c06fa9209"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Smb.conf access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/42f72b0e-b7e1-39b6-a52d-9099c8fa9d8b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"BACKUP DATABASE\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9172a48c-88af-37b5-9acd-adf6bc53f8f9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (8)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/207450e9-e88f-373e-b5aa-f6dfe5a616d6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ =\"'"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/830f09e5-e43b-3f0c-8eb2-f67c2ef91d7b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onLoseCapture() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4f0c4ca1-bf45-3664-8341-ed11c2c09e3c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( Gamma Web Shell ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4bbcfa6d-8d0f-3eb8-9207-9abc3bac40ff"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Email Injection (1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0eb3b32c-6476-346a-b61d-6e720d5d9139"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".fromcharcode (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3555b1e9-1fb5-36e4-a494-4c596a878a99"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href vbscript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4a8c01aa-53c0-3369-b718-ccc16ddc646f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ondrag... (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5b0bdbeb-4168-3e15-9aea-fd031fabd951"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: background-image (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/001ff512-4437-3a80-9af8-418913c01a15"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"processing-instruction()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4abf8f5d-0192-3300-8eac-652e8d2ca5c6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"SiteSnagger\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7d83a637-ec38-3336-b614-cf2f528ca566"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "xmlns:ev (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aac7db04-b36f-3e3c-bcc3-489d59f35b0a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".innerhtml (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c302b2d8-8e9f-338e-ac8e-9729fd2dd995"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (IBM EVV)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d1f6dd28-2b82-3cb3-9840-ad9b5d880d70"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onHelp() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ff03b1ad-3442-3a0e-92dd-0222fbf23df7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript buffer overflow attempt 2"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a7ce44c2-177a-35b1-b3af-07262e68d2de"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "@import (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f679ebba-6e76-3573-9cd0-9c80f2d1ed8e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"sys.user_catalog\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9f21e82b-37fe-3694-bccb-86c5a8f251ae"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".execscript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/adcfc151-9813-35c9-81cb-76fdac02eefc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select substring (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9a9a16d5-8cd5-367e-9728-1643af7ac3f8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.write (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5849fd30-2ad4-3b1e-b4cd-af9d873bf968"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ attrelid (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0389b327-62dc-3b39-a0bb-6baa671a81af"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT COUNT()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6da2346a-7bcd-360e-8324-54b4a399ed3d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onunblur (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ea0f95b6-3df2-3a0e-8255-b1fb4ffa9bc2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "link tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/130dd405-49b8-35f3-b9f6-37c4363d2c73"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select to_number"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b25b54f8-ec4c-33d5-b758-ec8a0c8b7353"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT CONCAT()\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c1c04730-53a4-3dbf-8e0b-ef0a61cca2af"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"*_user()\" sql functions (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/066cb4cd-e6ee-3e59-be7c-2e23927fa3f8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onunblur (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a7dd14e6-e642-3a4b-914b-bdf27beec81f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTTP Response Splitting (2)(Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/46bbfe91-537d-354c-986f-ca7802ac2dff"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT IF()\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d204f0d5-159b-3715-b6d3-1aca8522b43e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ syscat.dbauth (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/30d669b2-12a8-3a72-b8e7-1803934579e6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ CHAR()(Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/88622e4d-2a27-3723-9f97-48302a0313f7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ UTL_HTTP (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6722023f-9979-3100-afb6-9f37e73792d3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ UTL_HTTP (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d4ff98d8-81d8-3858-b7f8-b525daa7d9bb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysoledbusers"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/da045431-dd13-33bc-8e48-e576d71c5507"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ group by having"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e29c1d01-17b9-3876-9309-3d090eda2ac7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onkeyup (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/89937202-4f19-3b25-9dfb-de1ef6a1fa52"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"WEBMOLE\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c3059443-571d-30ea-a7a1-3fcf3eb3d40c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Samba SWAT Authorization overflow attempt"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9793022f-dc06-3240-a675-d27460d3a54a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"eirgrabber\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2b9b535c-4ca2-3372-b391-5e0f323a79b5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Acunetix )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/04f69cfa-5f3e-3593-b471-d17e5ee4b22e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Microsoft JET Database Engine Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fdeb94df-8650-3d31-a11c-4ee4b79cbc91"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "FSCommand() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/261d7959-49c3-3e4e-85ad-278181b804f4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( WebVulnScan )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4dc24af6-5172-3a2f-922f-b983aa5e7923"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (31)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6dff6ad4-f7b1-32f9-9cf2-d7bde588d712"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"; drop\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1fe214dc-3399-3d27-83f4-5996ae11f80f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onseeked (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/92d829b1-cc37-3549-b9ab-e81f8c13cb68"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "history.pushState() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/589b97cf-70e9-3d2d-953a-54254518870c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "launchURL (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f040d97e-b6d3-3af0-bdc3-2ea356ba9901"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".location (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c049ecbe-7f96-30aa-8f1b-bbb63d44e995"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xtype char"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6479b87c-7b90-3da4-8d1b-963872e25f7c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "applet tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e050c294-b340-3641-9054-87383adf4e6e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src &# (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/eeeace4c-1206-389f-9b01-8f74c39220d3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onOutOfSync() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/59240fe7-9fdb-3557-9f59-71984d1b9baf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onpagehide (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/13074d6c-8b80-33a9-855a-725144fe6429"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onunblur (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/25f81c08-d35c-3a4d-bc92-1c1ffe562d58"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_dirtree"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/52b52a14-ee58-3c0d-8f09-4e3f088e9022"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"ms-office\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6dfd20d9-65a1-3fef-ad81-2c2b07cb05ce"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Havij SQL injection (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aaeeaa7a-f622-3e3a-84c2-012a6dcad67f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Nessus ) - 1"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/90ef3018-b111-3a9b-86c8-ee57988cd0b5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT LOAD_FILE\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/90bf8664-aa99-374f-b0fd-0e7ba5ffb44f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web-Server samples dir access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1d37d5a6-f184-3e34-b474-20e81d5c65be"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( core-project )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7f33f8de-9524-39ed-9a38-434f20f15938"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic XSS evasion - unicode characters"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6d9e38d7-6930-3f9a-8562-1303b4756bb3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 3 (headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f81a35d1-1628-380a-a4ee-41f191e49e4a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "[document] (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c34daa65-4eb4-3860-8bb7-bad88b00ba53"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOMParser (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/da3fb95e-addd-3e13-82d9-47c3b7ba8508"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( Aventis KlasVayv ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bc12da77-1e36-320c-8b19-98872e18b5ef"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onActivate() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/abdedb04-6b4b-3f1f-a8ac-47224c2a0b31"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT IF\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/789957fd-968a-3df7-9c50-4fbeb77d4d01"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href shell (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0bdbc39b-7d90-3edc-8d8f-50378921eabd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "execute() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1d815403-df32-3dd2-8426-15dd9d80c637"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "link tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c8c3b3f9-48a8-3c64-b3ee-84ed326b6e93"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "unescape() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d42a70ed-c4ff-3b8a-899b-8fdf6c6433a9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"oem_temp\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/804ca799-7c2f-391a-9c61-4b1f19c3ae61"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "-moz-binding (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4494d26b-ed00-3c63-ac57-c521b20328c5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Remote File Inclusion Attempt include()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/febc9c5c-edb1-3f9b-8571-dd245c24b73a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( ccteam.ru ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cbe31bbd-fbe2-34fa-8c93-0ead3c222058"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"; drop\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/64ea3366-a89e-3355-bc68-90bfe3993a2d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "input type image (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a503872c-996e-3964-92b4-af2c4bd3c5a5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".FileSystemObject (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fef137b8-b086-3456-9050-08098c5167c9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ charindex"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b9e79c86-2813-33cc-8bb0-282e9abbb039"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"Expression::Type=Expression\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/363b6b14-75c4-36a4-acea-37bd1b43b390"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"dbase Invalidation\" Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d5a3df6d-3875-3c36-b044-ea9096d9350b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sqlite_version (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c9181ffe-99ca-3fb3-a6b8-cb7cf8528a5c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Parameter) (4)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/64373156-a2b4-3268-b6ab-528d8364e2df"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Educate Search VxB)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b4a6bdeb-2421-31dc-b9d7-4e6c34f2113a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Darkleech iframe detection"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e31e6140-1cc5-3741-88d2-1b5e4b707ab6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"' #\" (SQL comment) (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5cf2d021-fa75-377c-b44c-7831acec3172"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Fetch API Request)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/42703419-1aae-3c0f-bff3-cb9b9d0105e2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ charindex  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4114098e-ba5d-3c1e-9f37-fc4278373399"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SYS.USER_TRIGGERS\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5a9e2d6a-826f-30f3-a128-4f5dc35014dd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "meta tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9574691e-8bf9-3a21-9206-cd110828f888"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ truncate table (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/717b8539-e79d-315c-8ed3-6bd3bf34ddcb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document[] (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/682ec491-ba96-3a13-bb1a-cea2d7086a93"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ coalesce"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/644cd034-3515-3338-8e8e-6196482f64e4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onredo (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/39782c0a-230e-3dbf-991c-0d48c8c329af"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"IS (NOT) NULL\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/19a1d2d0-2f4f-3a9a-82b8-458da074b5e1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".old (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/35678c34-2745-3626-9dc2-a81c8d636f0a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"style :expression (\" (Parameter)(1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/23bc3669-fb68-3e09-950b-c2402727ca2b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "touchmove (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/37e69c4c-9b85-3ae1-bf0b-a663d8b8d4e4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create procedure"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b908797c-119e-31fe-8558-f7119e0abd70"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "UNION Syntax Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/73c00f12-a23c-30ab-92db-d12d4d0eedf3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ syscolumns (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6b8ce0f-a1f4-370a-9aee-d38453802d62"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (11)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/278f793c-edab-37ed-8744-d30381abec94"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( n-stealth )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/629d1edd-0599-3a6a-bfbb-bca0785402d3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ XMLFileFromClob (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c1728b0b-63e6-351e-8b1a-ae89c682b16f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oninvalid (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4108c43e-7611-38a5-bf68-583bdcd935ec"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: background-image (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b4d93c61-23da-3b29-bef0-2e9397ba139c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onended (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3f78d79d-b832-3350-84c9-80a5a8716b27"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create schema"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/47e8f076-4508-3e6f-b470-ef3009f18a96"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( S.T.A.L.K.E.R. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/00d13bb9-835a-39e4-b373-13c29356311a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ alter database"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/40b7b8f7-b380-31a3-bffb-147e8a5c3708"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onforminput (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/05561e54-a755-3077-a4d1-3f0207bb8ccc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "{:window} (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5fd76bb8-4842-33ba-8fd0-aa3d3f69b8b6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Nessus Scan Report Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c0d141fa-1258-3735-803e-7040ea2b29f7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onfocus... (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0db454d5-f3bc-306c-a8cc-41481f6b6ca0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onBounce() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/21e04154-c5d1-3e0a-bd86-1035d08af681"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (EmailSpider)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0579e79e-00ea-39b5-b8e6-a28019f25ddb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src &# (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6250e1c0-86a2-34a4-b20b-d0386f50ac18"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"element()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3d757a6a-5e75-3fd9-9139-9d5db7e94262"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ mysql.db (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/504fa668-dad8-38d5-a1ae-67e83718d6b5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "deprecated WS-Routing request"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/87455e09-146c-384f-b982-bacbc6949a9d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ textpos()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a32939ae-7daa-3539-932f-b5f8a37ca445"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (Jakarta)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4cb18a96-b9b9-3032-995f-aa31e22b15c9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "xml tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/39a43a17-6f46-3f20-ba68-78103ccea1ea"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "touchend (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4fe5dd48-a6e5-35db-8ae7-493b25b41bdb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"sys.tab\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a0f26614-2fdc-333d-aa6d-e56498ac8fa1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysibm"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0df50811-4ba6-3fd5-bdbc-7f7a4717bfd1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onsuspend (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a0f10b3d-2593-3b46-ac58-4bbde9a8f5bd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "touchmove (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3af8d3be-753b-3219-841f-f732bd4d790a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select data-type  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4c7f81b7-8d43-378f-bc85-24c72e672d9b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SA_EXEC_SCRIPT\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5416870b-2f18-3a4c-af8d-d5d124e42d2c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onBegin() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b5bd6d09-ea46-336b-b27d-9437b9c5b077"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ alter table (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4a28db0c-a899-39e6-a6f7-35f9b58c6f26"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"or 1=1\" (3) (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dcf1131d-1c3c-34b8-906e-e6bd8e0b5763"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malformed US-ASCII - script tags (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/599378ad-f7d8-3997-8fdc-dcabf66eca7f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( bind. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/13b8660d-537d-3de7-a6b0-59e2d5fcd883"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ syscat (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/93d2274a-abbd-36ce-9334-7761541b1507"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( jaascois )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4b5beb44-d92a-31d0-b204-cb270af073a0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "meta tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/894c2b28-b6c5-33ae-9645-dc2c981b3672"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"string()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/52233dcd-f9c4-32e4-b590-fbb9a56d4303"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ information_tables"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/68c27cb5-dc48-391d-9e35-dd912895796e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"@*\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6a44a866-e781-38b1-bed8-d5efe9d72766"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onstorage (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b43bad54-ceea-32b5-96a1-690f3e358497"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) F-Secure Policy Manager Server Welcome Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c28a6613-e26d-3334-bbd1-79be4b1fe72c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"emailwolf\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ac4d7ce7-f468-376c-ad0e-13a4fbd5ee49"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ order by (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f96645dd-0884-320d-95f2-c600772c02df"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "asfunction: (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dbc61c3a-b82f-3930-b572-39eecb044a76"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CURSOR:url (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b5c4ce91-f5c3-35d5-838e-69fdc0920adb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".addimport (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e99649c8-bfa0-3811-9b5a-53f4292062ac"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop database"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b465d2b2-ef2b-368a-a797-29818bde7dc2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onScroll() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f0e578cf-0cde-3907-b889-09df509e7e04"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( RHTOOLS ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8c82f4e1-7238-3933-81bd-f3bc652ef28f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ information_schema (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/db7fdc95-f399-3a07-85aa-ed624a8bfdf9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ondrag... (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/adc9bd61-537d-3411-9ea5-49d6e085b852"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "OleDbException Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2fbd3fee-3a78-3011-a414-192efec30091"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( PHP Commander ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0d73df6a-a9d6-3533-ab75-c1201b702af9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Sun-Tzu )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/88bded95-88a8-3376-bb79-a9c73946c5f6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".SaveToFile (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ec6b8102-276f-3351-b726-42c43cd14611"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"automailspider\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/50067bcb-3bc4-3fc4-a014-a6fbfe8895bf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"SQ Webscanner\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/588ad31e-169b-3588-9b97-8aa0f24ac3df"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop column (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e747c036-401f-3c2a-bd33-5e6112077a57"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a5d6c355-a37e-3adb-9300-54fcb357d85c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"netants\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6b375003-2d0c-3c04-bf1a-cf215f676c22"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /juax. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0d76244b-7390-35a8-815b-40d65fefcee8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "link rel stylesheet href (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fa852977-5d00-3e4e-a8fb-4622464a4a77"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ononline (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/809228e2-57b8-34e1-aa06-8448bfd9de7b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "getFromURL() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/51ecbb6c-b1be-3cfd-b540-01f3b9e6912e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"select --\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/be7f30d5-46bd-3e5c-993a-b6603d6a8381"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".send (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aa2c3776-9b4b-3698-8a5d-ee0d82535d95"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style list-style-image:url (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b1130cad-55bd-3969-b3fc-4b833e96e18d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 4 (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0ca08c62-c16d-3479-81f3-cec8cf3a9324"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"CREATE USER SET PASSWORD\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6d59dbaf-19db-3cec-9571-c0d8a09a858b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create function (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a134f33a-47fa-36c2-9c8e-8423ae0b3caf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( WwW.SaNaLTeRoR.OrG ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/46ca4e20-c137-35c6-b6f4-a0b12174a48a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"style :expression (\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f93d929c-c175-30a5-90a4-e7c5e844edc7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "setRequestHeader() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6aaf5d1e-868f-3677-8258-590d5c3e3a93"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Webtrends Security Analyzer )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2bdf1186-2046-3133-885d-9555a04ec8e8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "FRAMESET tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ff3650f2-ba56-30bf-a615-e83c319a8822"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "img tag: src/dynsrc (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/98accee2-37ef-3185-843e-18f50d1a6f8e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ononline (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4eca6400-fc7e-361d-9d45-e30ff409fffe"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onControlSelect() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aaae338b-de3d-31de-95cd-dfcad4f81567"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".createDocument (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0a074c88-200d-3889-809d-7868364a815a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CSSHttpRequest (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/17e5107a-a33a-32e1-b335-ef9a83ccd692"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "data: base64 (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/58fd66f7-6048-332d-ad07-0fd7a34f5331"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"; shutdown\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4ac1b6b0-7902-3736-8fac-70d72adcf6a9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"end-quote select\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b9cdc9c6-0be3-3e51-a4e6-4455828300a8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( shell.txt )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6798aad6-e0f3-3d47-8cf0-7b23d70b7ce9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "button tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/df87de3f-607a-3c12-97b0-016785c98967"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"BecomeBot\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0f9606b8-e8c3-3b72-8dd0-88ce5d5092b1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( brutus )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/17490c67-5b66-335f-8a3b-9d43a6121965"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ syscat"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9b4258bf-7b59-346a-8456-9c91d45f11d2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTTP Headers Injection (HTML)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/be9f93e1-b721-3fbe-a846-866ce2aea192"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src javascript (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b1864354-c7c2-3ee3-ad77-50ba4e1392b1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "= document; (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/097d746f-0fea-31e1-a165-d48d4e4897a6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"UNION SELECT\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/22490dcd-538d-39c3-bf24-1b9b1c40de3a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onactivate (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/734699b5-c7a5-367d-9d2b-e84c4c3d35f9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onLayoutComplete() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/627192ec-8504-336e-b78d-de9d17eae948"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onData...() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bbdaa2ba-9ac7-3b4c-b3e9-7850820d5dfb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DoS tool (SIEGE)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8c232632-da5a-3d4f-a268-724cfb1fe15d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onoffline (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/21c2f577-5f71-3b23-918a-8ea1ab576443"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( absinthe )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1be9e731-759d-32ae-9667-9375d7c72e36"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ REPLACE INTO (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bed4c7a5-6cc0-3b55-baae-f4773e794297"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( w3af )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d2d4a1df-94da-340d-8c7b-44d009f505fb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onunfocus (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/88c0d511-6dbe-3fcc-baf4-23ded9a0ce23"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ImageMagick arbitrary file read (label)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/91af3672-365d-3fd6-824c-2bbe0fb4d762"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Cenzic Hailstorm )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5cd9a189-98c6-356f-812d-a9eb175c5320"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( Remote Explorer ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c7c651d5-f883-3cac-96ae-f0dfbe36df0f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ alter column (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3250a74b-f87c-3d62-84ae-49bafb2fa74e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"autohttp\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f5e98d9c-ce9e-3a53-8d4c-e1629d50af2c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' AND 1 IN ( \" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c85709e5-48fd-3efc-882e-dbd3d023fcf7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onBefore...() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/60ec3cce-8a8f-3e92-a25d-85a7f574c687"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (12)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/02f655f0-3ca6-3e9f-8eea-16955eb7552c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onbeforescriptexecute (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b5d35844-6383-36c1-9abd-0450ea95e8a0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysobjects"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7f1a3067-8add-3a83-8c02-d94f06f843e0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /lala.ph )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c61eb3f2-e4ff-3a64-9ddd-48c8a8ca6729"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (panscient.com)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8d8e2d24-b6ee-3ad8-ab07-bcd9bc87a1c7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onBegin() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/373f045c-f0e2-32ef-bba5-c47a0c65c8ce"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Session Fixation Attempt - 3 (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5baa7d3c-2064-319b-9f30-5b0b08e72915"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style display:none (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4340cf83-bc73-3f4b-8748-126691ddf98a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "FireWall-1 error message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8c0dcb50-258f-36d5-9748-f09baa1cccbd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop table"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/821ca565-d113-3cd4-8b33-c7fff7ec38f5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select ascii  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d409b1b5-0081-3bac-8f97-56194ef957ea"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "STYLE : behavior (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f75d222a-7c2d-3119-a32d-fa7d4eca3a57"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT COUNT()\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b1988c2e-ac37-36a6-bdcb-db2f0b23019c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "createtextrange (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d9d7351b-a6bb-3e2a-ae10-88aaeeea8378"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"bulk insert\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/67fdba23-12d0-369c-8ef0-95b46a42a956"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "formaction (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9b2a21e0-8f53-3e01-99ab-857665ea784e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onProgress() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a16c3db0-bdf1-378b-acaa-7a394f56ff6b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_regremovemultistring"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/365f1423-69d1-3467-ac7b-661a214ad5bb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Temporary file (\\\\$) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b5433b31-c897-377c-89d6-315ba5e036b4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "activexobject (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d8508a55-a90c-3aef-8800-05c44449a2b4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "data: base64 (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2d590673-0b80-3e83-bb5e-5960a3a79dd9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Escaping server-side escapes - double-quote (Value)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c8d83cf7-2652-3ffd-b3b7-6596ac7a3c69"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Havij SQL injection (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4f806fcd-81db-35df-9bbc-834e4bc61c41"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sp_makewebtask"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e58b46ff-9be5-3a99-9bb2-c12019d8e989"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Remote File/Path Include Attempt 4 (dir param, http/https)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9bd5a987-c928-3465-afb7-7be9bd6194b3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Remote File/Path Include Attempt 3 (dir param, ftp/ftps)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a3cafa32-3f8f-3751-a65a-87851a86f127"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onDblClick() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/29428a96-45f7-39cd-9847-44348e714939"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysfilegroups (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0e753dc6-98ca-3157-b25c-666098b06624"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( pangolin )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bf45dab8-7ed0-31b1-87e3-d788148d7300"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"preceding\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/12108820-f356-3e1d-8bbe-7454a291d580"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "link href rel stylesheet (Parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6e2c9a90-e429-3560-80a3-f81af28a324e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oninput (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b97bf198-f811-3f82-8ac1-1b2ee5e1dd7c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"order by\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/45f2e78d-e4b3-30e7-8183-0c15edb7ecc2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.form (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3d43a0b5-b607-3cce-9050-73e8ae8dfef9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop procedure (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/27ba9bcc-f08f-375f-9a94-afbb88e0d7b8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create procedure (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/403f3c3b-7658-384f-bb82-2b91f410632a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"' /*\" (SQL comment) (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/460857ce-e4d7-3f14-a4da-c59b69452235"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ into outfile (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d3017eb8-17cc-32ab-a63e-bcb745ecbe02"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"mid()\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8bc6321e-cc38-3349-b508-fa1bb4e5721b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) System statistics Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dcbee2ab-5c7a-3e97-b805-4bd82db26511"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href shell (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/028eec8f-5829-3065-a2c3-672d93b30e0e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"IS (NOT) NULL\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/159a7324-57b2-3b00-92c7-d0b330a2c00e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onPaste() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6b474bcb-bc69-37dc-a6c3-264e1f087471"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Pushdo botnet traffic - Probe request (1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/70117d0f-bd1a-3a1a-ac56-c8231f20048b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT CONCAT\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fe746922-d1e4-38a1-8fba-98269f4e7e2d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onbeforescriptexecute (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9c51989b-fdaa-3d5d-957e-40bb49dfa71b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( r57shell ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/52458682-a3e7-3db3-bdf1-ee6272533675"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ print @@ (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6dd8c418-1038-3415-aa0d-169fc09d8f99"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysdatabases"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9e911588-807b-389b-b8b7-5b270adbdb50"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onpagehide (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c3d265ea-9dbc-3214-ab72-71abdf35ef43"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic buffer overflow attempt 30"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8973b5cb-4815-3dca-a990-5038cdc37a00"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CDATA injection attempt 1"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/48083c0b-a072-30cb-bf34-c6bdeffcbf19"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ v$database (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/12b64301-640b-313e-92bf-be8e8e40c983"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onFilterChange() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c2a47003-a04f-3ade-af93-9d3e6cf0d355"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onoffline (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/272586ee-903e-34fe-a3fb-8dfab676e4ad"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DoS tool (ab)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/161b8b21-a87a-399e-a6f9-98fc958bc21e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \"../\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e60a9d3b-ce50-3f64-a503-46eae215f819"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ v$datafile (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8129f632-556e-3f82-ad0e-74277b719826"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Statistics Software Information Leakage (5)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/00d9b407-dbe5-312c-81e6-34e34e2687c1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "{:window} (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/95539dd1-d85b-3cf8-9240-87b3209a843c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"CherryPicker\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a81f14ed-db9b-36d1-8296-ecba37b6c738"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onPropertyChange() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fe7c90b7-6896-3e2d-a226-337c801bbbdc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ constraint_type (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/04964628-c68d-3a2e-8d00-a0dd24579b79"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onpageshow (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bedb20e4-14ae-36cc-ab9d-33efd5e17d0c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url shell (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8629e0c3-df89-3606-abb0-932232d3e09e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".createDocument (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c7224097-1485-3b01-bafa-032da4a32387"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( PHP-Terminal ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b40ebbfe-9864-37e4-b943-fb6464045c20"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onFilterChange() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f1dee556-9d91-3c5c-8e9d-32fda24af4fc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \"/..%c1%1c\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6dd9a73-a9dc-3155-b17a-b030c0dde7b8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href javascript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cf03c8e4-3dbd-3f13-93c7-2f067b94e15e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onunfocus (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7016aca4-c2bf-33b5-8797-b791681b0c62"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) WhatsUp Gold Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/38b025fe-4779-33d3-985c-b806fe23e9f8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".send (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6f841840-a8a3-394f-ad64-3ba53d1b32fa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ into dumpfile (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9b957380-6645-39ba-ae7a-9eedc1fd164d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_filelist"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/572eb7a4-25c0-3d94-93f4-9e959a279e80"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysconstraints"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ae8d4cdf-e4eb-3745-8c3c-df3421224e2e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Fiddler Web Debugging Proxy"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6d945b8e-6334-34a0-acf2-3267aae3bcd1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop function (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5424f567-26b7-3b0c-891a-15fb7395ad6b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ group by having  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c2e216fc-a660-307b-b0cf-09f99b87a038"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ attnotnull"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9f512428-3690-345c-882f-c9a10bc5ebbf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ msysrelationships (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/36576345-4cbc-3447-8d20-a9ef51f1d329"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style list-style-image:url (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/33c2ee7d-6620-353f-9c75-5a4084452bcc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"document-node()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ca26777f-194c-39e1-8b48-14941c6e9118"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( wapiti )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/98374ce1-a483-3a1f-8ecb-0af2e8ff4713"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "/passwords/ access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a1271d2c-035b-3d8f-b347-88cea529759c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like ' or 1=1 (6) (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/27289329-28c2-309e-b77e-b8b06c467cd5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XML External Entity (XXE) injection attempt (Content)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/797e0e2e-ed23-3400-b4fa-7489294dc80d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "LDAP injection attempt ( objectclass )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/68b269c8-0e7b-3e39-9e15-11d91799eb2c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "history.pushState() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7e203b82-71f6-364a-8779-68c170d6af99"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Morfeus Scanner )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/429a8319-80e5-3002-85e4-adea63d27257"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( .k4ka.txt )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/718f959b-287e-3603-b624-5ed13ea4fdae"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ REPLACE INTO (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/96b9d6ba-b9a5-34aa-bd52-f838ca117945"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web-Server log dir access (/log/)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6e2ff7eb-7d01-31ab-99f4-65dfc527a934"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT TRANSLATE()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2fb99dbd-d919-3830-8510-8cdd99fa0b74"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmousewheel (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a89c0cca-71b7-3624-a273-2fa8a32d76a2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( DataCha0s )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/64216769-a398-3dbd-9cd9-a9ceb9d569e8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onselect... (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/955a1372-4a8e-3a35-9bf6-10c42749ff9c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( PHVayv ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ac8da6df-2958-390c-ab7b-ad8d320531d6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onshow (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ddfc0acd-4869-3c1b-8f90-fad65037a04f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onoffline (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e41b7e13-ed6c-33bb-af96-945c6efbf585"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"snoopy\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6f5f1cbf-03e9-324e-a605-acf1900e0599"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe httprint in URL"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b94ffed3-9a06-3c13-94c6-04c64f40a522"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Acunetix ) - 2"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/955bf629-c1f7-3516-b10b-2eef6d704561"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /linuxdaybot/. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/547f7f3f-f935-3d12-9d3f-f30cb6409d74"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"reverse()\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0f3e6d4a-fbf2-3c34-b371-d8ad6c268307"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = application / x-shockwave-flash (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c76c2c23-578f-36f4-944a-513a338c2eb4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \"/..%255c\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/38a112fc-db4c-313a-8646-1583779ec8d1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onReset() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6b49a61b-8bbc-3a70-9a24-e33375dcd165"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"; shutdown\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/90131f48-2ce0-3755-93f3-8006f43346d6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop column (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dfb73f11-cd6a-3c8d-ab40-378b0738d201"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"select --\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/358db42f-b1a3-37cb-80a3-e23abea076c8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HP Web JetAdmin"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cbbbeff0-4fe4-3474-a653-e89149e3e9e4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ openrowset (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/177d2322-6b7a-39b5-a376-67e8c7148610"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmouse... (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0a8089a1-ac34-3542-a7b5-35d57cf3769b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"Nokia-WAPToolkit.* googlebot\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b53b6b8c-32b7-301c-8d0c-5e832b0e0321"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "livescript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dcfd39e4-e577-32d8-9957-b3751c2fb3b3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop column"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b302ecde-833d-3e21-ba0b-b266111c1090"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "UNION Syntax Error Message (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d5f43da3-ad25-34f4-b8a8-4703801a2aee"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onBefore...() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/92803a4d-db59-3a60-8b9f-4cc6511155c6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "mocha (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/859efb98-1b0d-3a7f-8a1d-bd7114f6df17"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onStop() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/59565eda-d292-3e31-807e-c3dbfaa2feaf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ autonomous_transaction"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/faa662eb-915d-321d-b32d-088013fbca4d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Remote File/Path Include Attempt 5 (include param, http/https)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/124f0b2b-f460-3c0c-bd5f-f70fab873573"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ all_objects"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fc23a1bd-346a-3e88-a8d2-f82b4e0ae722"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"nullif()\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d5e452ac-95ae-3666-95f4-4786d9dc7780"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ mysql.db (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1528022b-8932-3d9f-850b-2eb5adfdb9ed"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( PHP Shell ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dbd65858-f038-3934-8b02-8670259b24f1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "BeEF injection detection"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7e712612-92f7-3dfc-9ebe-e21ffb4101a9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ CHAR()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f4cea602-64f5-362d-a2a1-98cd31141434"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop trigger (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fd3cf1bb-34b7-3aa6-90f1-0c4e3a794c24"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"MySQL comment\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5a17e6a0-4f42-30b9-8da6-1c5acfbe706c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onforminput (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b997c742-5c3f-34cc-afbc-b314e31fe94d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "toString (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2d398c17-772e-3f72-bad1-136b0cfe9b6d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmessage (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4e3d8cda-6ea1-377d-93a8-b4a2695aa83f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"index of /\" response"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/432c38ff-8c76-3b05-8d08-f7dfa20bbec1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Joomla SQL Injection Probe"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/44d515d2-44af-3288-b397-7862619d6d2d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oncanplaythrough (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dc0e6903-d22e-33e3-b6f1-af3f04e0ab75"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XMLHttpRequest() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5f2311ec-0ef7-3391-b18a-224637f0e2a7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQLOleDB Connection String"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d32bba4c-9885-381d-8d5e-de5b91386c17"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onplay (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5f711b33-c7e5-353d-8cc6-e6156e69ed6e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (PHPCrawl)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7c364a89-996c-3fd7-9e7c-75c3889634fe"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onwaiting (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/23d5223a-66fd-3ca4-8950-40a1ce33eeb0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.write (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c6856e44-e29d-3e45-b7af-5f73191339e8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_terminate"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6ef92385-ee65-3640-bdad-6b4dcb7e2219"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"takeout\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/823ccdcb-9b7f-3848-b76b-9c44b650d347"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Listing (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f6fea06a-a2af-3093-9a62-331e6fb41eea"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onratechange (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8888d7c4-a771-38cd-a8b0-3fdee13d17a6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onLayoutComplete() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d12c724f-6626-32df-9f92-1f97e7e96197"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"MySQL comment\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8cae51a1-34ff-34ec-83a9-f4260929bf69"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmousewheel (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9a42ba3b-2371-3a6e-abff-8a87dec2aa8c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script tag end (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/23c57406-7757-3985-9236-361fb7dbce33"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onseeking (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f1438067-35c8-3a68-ba4a-c53e59d77646"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ v$database (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1c0232d7-4b63-3602-b7ba-3a57c21dbec2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = application / script (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fe282484-af08-3f31-b126-dbd1c2ad7bbb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "touchend (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/33c39a4b-697d-3e7b-9e1d-13a63370773e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onActivate() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/662b319d-2868-3ff4-9d6a-2615e039d5bd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oncanplaythrough (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/15d1c0d0-0aa4-3a5e-98c5-2c634ef87f08"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onvolumechange (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fed90fd6-3527-33ae-80e6-942956043ecf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ attrelid"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d1dd0234-0e34-398b-80d9-8d9ec7d38e5f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( WebRoot )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/78ec5d89-2f0f-3302-bc9f-b1933b632bfd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ instr()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3a928cca-5d37-3f5e-ada6-e8affbc91c30"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ Xmlclobfromfile (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5956258a-2a01-33f7-bae3-f70dff5a16bd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ encode() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ae6d7c7b-4900-3c6b-a832-5d73d1f0b363"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Content-Type boundary evasion (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f6704b2e-1edb-332a-9f3d-d770a4a87ec4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url vbscript (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8b4a0db5-8dc7-3b18-912e-7b100f4fcfe6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Remote File/Path Include Attempt 6 (include param, ftp/ftps)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9843ccdb-3e8c-391d-b54d-25a44808ecd4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onTimeError() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e652b74b-bb6f-3608-b738-22c12474da5d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onFinish() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8437f0e9-63a2-33e9-b788-b9e49744d123"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<![CDATA[ (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/73080d11-3c20-3d37-a314-11d9d9624ed0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"or 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/202d5fbc-bd9f-31f8-bb31-cd53b731d112"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onCut() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/41820270-55d0-3df8-9587-4678e6926a95"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( IP HACK TEAM ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a7c2e621-91fb-3f54-858d-6e2d73d95d29"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: background-image (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2e5a6c00-3597-3fcd-9979-b66acca04d02"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( black widow )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/12dfc951-4e14-3113-a919-37719e847e00"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( =http:/ )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cdb42e98-02e3-3684-a338-07bea0b0bf62"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onStop() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cefd57c6-34aa-3d77-a1c7-24bed4f13e93"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onloadeddata (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7baa222b-e36b-394a-993c-145446729bb7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Kenjin Spider )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bee78100-52de-39f0-ae06-9b8d842c724f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onstorage (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9a41642d-c25c-3460-80b1-3ec8d5d7c201"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"UPDATE SET WHERE\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f7fb2b0b-c999-382c-ae10-dd995fa1d4dd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web-Server examples dir access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/51b8cbc1-b18b-32b1-be6f-f9508f489728"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( CGI-Telnet ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b08bae92-57eb-3cf8-9672-3f4320c42ffc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Scan - IBM Security AppScan - Standard Edition"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8e8834f4-42b1-38c4-a311-70523e18e89d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like (1) \"' having 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0372145f-b086-351e-a016-8a83ea443114"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTML entity - &#x... (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dce7f7fa-a5a8-3dd6-a689-f5183f78b564"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript buffer overflow attempt 2 (Response)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5e75af27-c4c4-3eef-88b8-5101613d8162"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ bitval (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/978cf174-dfe7-3e03-8792-fe739e5396e5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onplaying (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/615dd037-1516-3056-b874-51c4773af361"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( DirBuster )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c4663b32-0260-3296-8088-dd958b135688"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( INTERNET EXPLOITER )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d18c2e39-3ec5-383f-8401-9795387010d0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"download demon\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6eeb04cc-eceb-3356-95d9-ac5e286bc03c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onFinish() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5f4dfbd5-879f-3135-bbc9-238be3fdc0f8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "textarea tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e596d9a2-a0a8-300f-97a3-d9a674324522"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe (/noSuch)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e043d40d-386c-3cda-a539-6f496020edc2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ alter database (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0e66e17b-cd57-3463-a433-20dba554fffc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) PRTG Traffic Grapher  monitoring results"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c607c2f8-7af9-351a-98b8-990897c84adf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"Telesoft\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fbe2fbd7-a562-32c3-bed1-018dcbf3f0c0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt base64 (parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a307facd-f78e-36f4-91fc-0e8b9bcee1f5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src vbscript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d573d8a6-fbc8-3c37-b084-f2af4376904d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "LDAP injection attempt ( uidnumber )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d5736a66-bdd2-3dee-b321-4f4c0dadd04d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "@import (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/abdc16b1-ae25-3766-b764-2239d63c3c18"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (FSurf15a)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4a7e82be-94b0-33ed-927c-7b9143df5733"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ encode()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6083595d-bb1f-324f-87b0-27b7beed1164"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onbeforescriptexecute (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3c974d4d-455d-3883-87ae-ef5bfca9d966"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onMedia...() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/610b026d-7b99-3080-9032-dddd12f6a499"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ truncate table"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4ec508d9-6e06-3049-88ac-d8ed64557811"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Full Web Bot)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/83a38730-4169-3213-8b08-e7b618038bcf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"local-name(\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ff8b369e-69c5-3dad-b788-abf077a11b56"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Toata )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c58e9001-d68e-38b3-8dad-194adf080c1c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onredo (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7928c450-49b1-3f73-9183-ee478e05e226"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /r57eng.php ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7c21f1b9-f5ef-37cc-afbc-e5b004355f0d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onAfter...() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8db8c03f-ed0d-3f8f-91af-6d2302f451ce"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onDeactivate() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/181abc33-3cc3-31ff-8340-d6e66f84bdfd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onloadedmetadata (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2e5e1253-740a-3aa9-95e4-bc02ddecc9b4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onended (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ce3c157c-f25d-3c74-95dc-b265656b2f2d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Uniscan )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a4c5aa34-661d-326a-995f-002c221ef03a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sp_prepare"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cec531ff-0f59-37c4-b54d-f1705fc66be4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ msysrelationships"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b145f895-6411-3529-bf2c-9c3b66296ed6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "object tag: codebase (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2bd3c6f2-f4d6-3c9e-aeac-23d653061d01"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<EMBED SRC (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3848a9c8-201d-30ea-a1ab-72d5355040fa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Attempt to access to local files"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a3faea99-2369-30f4-8e83-f64a23d9dbf2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script target (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/431aa634-ca84-322c-b9ce-c711610593b9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"select --\" (Value) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fde5eba7-4966-31cb-b37a-cf2755e93982"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ into dumpfile (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/29d3bade-087f-3f4a-9125-8ac098996e59"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Ntop Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/faff95fa-5643-3d34-9d70-f081f4663d1e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onended (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5c2ce18c-082e-370a-8567-3562408c005c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onReadyStateChange() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a8df521f-05d5-3921-9bbc-2ef1e18a19e6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "eval() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4f8b057b-eed6-3d41-b4ce-c163d4c02335"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onReadyStateChange() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/beab5dba-3832-37d3-8c2a-f7656a4e11a1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onstorage (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/724fa602-314c-3460-9b15-154950680d11"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"*_name()\" sql functions (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b1570cb6-ba70-36a1-b2aa-3ac44e68809a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like ' and 1=1 (6) (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/63973c55-5bc7-3049-91cf-65807dc1c304"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "xmlns:ev (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/42738b16-f73a-3d5b-bf32-5fac8f2079ea"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select to_char  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0f964ba2-35b2-33b6-ac79-6d562e0e767e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ into outfile"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8e2e1ca1-9592-3fb3-9a32-dff74bfcb46d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "valueOf (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0f9667f3-05b0-340f-8e33-0413726dd317"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"Black Hole\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/874c2547-30f6-3ec6-81b9-bfca28c32fcc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"*_id()\" sql functions"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/74380976-ad80-3d68-9c10-b03b92f69cc1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( paros )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cb9e51e9-6c73-3008-945c-5494c5eb7454"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create function"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/795a43c4-d353-3ca8-aeb9-d38319ff37b4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.write (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e12b03da-bb9e-307a-baa1-b1cad2f976d4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onReverse() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0b015e56-b4f2-3401-8573-605278c70763"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Javascript Entity (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/28fa635f-e556-3c9e-bdec-08f02e034f4b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"/pls/admin_/help\" access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/19de4b8b-6147-3c59-890e-eaa12fccad3d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (EBrowse)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/77b1d434-860e-393d-b777-4d0427c91b2c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "activexobject (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b6e9e128-3d3f-33ab-827f-fa9940e6fe7d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"POE-Component-Client\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ebf6b712-1c0e-34ca-8240-e1708e5438fd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"WISEbot\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9f777d0f-941c-3a19-8fee-66b4d39b201f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ CONVERT( (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/30b009fe-091a-3f7d-834f-aef78620fbbb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysprocesses (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2a051b8c-aaa3-35d6-b656-c83ca116cf5b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"Butch__\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6ea726e0-3df4-3fc1-a212-7601862d3fb5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ruby execution attempt"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ef195191-a37e-3c5b-991c-99cce5709364"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "@import (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fde9012a-19b7-305f-bd6f-4fe92c3c847b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \"/.\\\\./.\\\\./\"(parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6a69038e-c14e-3e89-bfb9-0368519fd55d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( webinspect )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/97f09e6f-0c8f-3fb7-9c18-e01c5bb4ae50"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onpageshow (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e84e7980-13fa-3afa-8ccd-c6b5c888dc2a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "STYLE : behavior (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4d153257-e0c8-39cd-a9cb-577c45b9b6d5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Remote File/Path Include Attempt (7)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/61931331-0957-34f4-831e-01af9a8c83ec"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oncanplay (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f531c617-04dd-3c57-a6ac-33a0b47cf534"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"/soap/.../spy/\" access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/53696837-0f87-34a4-bd2e-0ec4bb2cb006"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "launchURL (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ef02f382-5737-3cda-abd3-4d58edef9a05"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web-Server log dir access (/logs/)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/221b2278-b0f2-3c76-ace4-214fdf7bc302"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' AND 1 IN ( \" (Parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/27254704-e786-35d1-9841-56d9532b63a1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<BASE HREF (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e0017a04-96c8-3e71-a204-a38a1c8bf495"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".bak (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/18657cc3-495b-33ed-a9a8-f681e83d9f00"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"begin declare\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1c50a2bb-5c3a-3cf7-b10c-adfa2c09fe2d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SATENCRYPT\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e8b2a054-8b2a-3d96-ba73-6143614ad43e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 5"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/356b80bd-51df-3033-bdd2-2c2a8e04c56d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "STYLE tag: binding (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0d63c303-f1b1-3283-a238-d9a268ed0e06"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ REVOKE FROM (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dd5be24f-5bc1-30bf-aa19-57c24e11b6d6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xtype char (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2f271386-3abc-3735-a941-b5b5804f3332"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onloadedmetadata (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4bc8f0cd-c90b-3dd5-ae04-03e7676cb92f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"namespace\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/189f2f53-496b-3bdb-b5d6-d7b6b70ccbe0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "{:document} (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7cad2308-613e-368f-94f5-b0fced385ad9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".ShellExecute (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/75ca11c2-5cd9-3172-af5e-e0ea7c9fca8f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"string-length()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/36c09482-ddde-3c7e-a9c7-8af45fb7bc98"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Internet Ninja x.0 )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/47d25def-0ea8-3e20-8664-620c87738360"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT FROM\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/70362063-cfc6-3dfd-b186-2cdc0e618d7c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Email Injection (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/08552aca-4c9d-39af-85c1-aaa97d1938c1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "settimeout() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/472b146f-8967-3fe4-87cf-7e0c52344fbd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "autofocus (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/439df121-2c98-3463-8242-d088f17c7c4e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onratechange (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6a80b76f-4e43-3e59-bc9c-0e8baa8ee1e1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: expression (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f5d932e3-ab08-32d4-9302-c877873196f1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href javascript (URI) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d76e62b1-3c20-3626-87fd-e901a6d29bc8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "copyparentfolder (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0fe5e862-56f5-3315-bf55-4ebbeb256758"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"DROP SCHEMA\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/823d8a03-7619-3686-a516-84b0cff860b5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "createtextrange (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8cd2aaa3-9df6-34ca-b287-0e135fba167e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"DTS Agent\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/18635f63-14d8-3d71-8853-93977eb05d1b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onunfocus (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/76b3fcc9-3fc1-350d-8d4e-b918747ef360"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onkeypress (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/441a3161-7196-3360-afeb-6ed7ff145ccd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "#RefRef DoS tool (1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/da00bdd6-8cc2-3c79-94d0-4d2651c288ad"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "escape() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a07d17dd-2283-3507-82cf-27439d798610"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Escaping server-side escapes - double-quote (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/530c260c-08bf-3589-8b9e-f45808d8fb5d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 4 (parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1ae752d3-3cb7-36f6-95e8-7cb4cd54fbf9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url javascript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0894251c-f128-304d-bb93-61ae17e3555c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onstalled (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/454178f6-cb0c-34bf-9b9a-ce8dda82a9ca"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onReadyStateChange() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/924fd4c0-7741-3b12-bd40-b5b7cfb5e413"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onDblClick() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4946912a-c0ba-3825-98fd-f2df425d456b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /kaiten.c )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7b975dc4-76af-343f-a3c7-45c5b03e25a4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onAfter...() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/efc39364-bccb-33d7-9d8c-91293c0aef7d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style display:none (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/48b26ba3-bd15-39cc-901a-70a3b013840c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onFilterChange() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/65716a4e-2a0e-3e6d-94a6-41f582162d39"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url ecmascript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3e2c35ac-81e2-30d2-9bce-336e4f9ba3f1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( phpRemoteView ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1a6efc60-be34-3457-9a20-6fe834b88a12"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"emailmagnet\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b3ac119d-5e20-3c0b-bf67-95f1b5e90e4b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"and 1=1\" (5)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/695351f2-d923-36ee-9c6e-5a67279d6eb1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( nikto )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8948e369-c9f6-3a8e-bec7-13581ebd1ce3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "iframe tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4f2fa6b8-f3a0-36a0-81de-f300d4d807bd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /lol.php ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b7df3068-af34-3ec8-bebd-f2d2a586d1e7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Statistics Software Information Leakage (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/eecc7e70-c8d2-3a8d-90e3-f5a61c9112aa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "getspecialfolder (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b959078e-5913-360c-8421-d24475b93a8f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ waitfor delay"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/66d212b2-8075-331b-ae77-35f18a1eda50"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "setRequestHeader() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/24328329-8f93-3c94-9833-2b18d3a1d5b0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Javascript Entity (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e4bc4231-a4ab-3293-acd8-6d402afbbaf2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onProgress() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d9c3e6b1-f9ef-3949-b0cf-aa245645c669"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "{:window} (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7d6450bf-3ff6-3f91-8ccc-1ab085b8308a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "{:document} (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/42019c45-bb0c-3c41-a9b6-323cbbf06423"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Analysis Console for Incident Databases (ACID) Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3b58c3b0-fbe3-3dfc-ba63-fd26076d58dd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onchange (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7d7acc6f-2bf6-3304-a6c4-f1bc8cdf6387"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ pg_class"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/39abf104-f68f-3337-a96b-f2f7cbb790f8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( ati2qs )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4ad89944-a3dd-377d-a69d-37d677b1a308"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"child\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8daa7e32-5da4-3dcf-be74-8739e9e0f33b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmove... (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d36bd6cc-4c83-34ee-86f6-93d18d7b53e8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Multiple applications detected in Content-Type declaration (Form)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b5de8a27-2b89-3ee6-b9c0-1c4dda05b3bd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "= window; (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/05b336b5-3b51-3659-a250-0a1d573cc1e6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "toString (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c6a46c06-d1f5-36d4-8f82-5b79d1a1eb3b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".FileSystemObject (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/797de41b-033b-30bf-acaa-2202ab1d7c51"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Barracuda Spam Firewall Welcome Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/634f246a-ad18-3587-9b21-368858a45d1a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ontimeupdate (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1ec5292b-639f-3836-bd26-f6111118010e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Grendel-Scan )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f59ff8ee-0a38-3d31-830c-188598afe81e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"if(Expression,value,value)\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7a8b487a-c1ae-3835-8788-ed9247d0b57b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src ecmascript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/79b1d240-b1f3-3159-9b29-3c042836a517"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt (User-Agent)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/252c826f-33a7-36c7-9f52-77894fb70c79"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: binding (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/25ecc59f-9794-38c3-8f82-1eccb4ea4707"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url ecmascript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/74e6586d-6039-395b-a62b-12aa1757eae3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_regaddmultistring"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/595f19a5-387f-3873-acdb-196a4c2e8ab5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src javascript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/284d297f-dd1a-3a58-830f-8d3c1c483184"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = text / script (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c5c44e04-3f9e-395f-bfa4-57187ddd4f74"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysdatabases (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4d1cb067-ea58-37e3-87f4-74aed13165a8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onError...() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f2edc4ae-9758-3f24-8926-d5c56414d88f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ BENCHMARK (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fd490688-3568-3d4a-b1c6-f472254928af"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT when then\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0da0e20d-8792-30b7-9c76-82e036e34037"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /tool )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3ef1ae8f-a2d9-3ab5-872e-ffb60395925b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onSyncRestored() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f3b5a3a4-ae1a-3e15-9c10-ab4d7b450c97"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"descendant-or-self\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ac46bc8a-69fa-3bda-b034-ea42806c02ca"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onseeking (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2cbf6d38-ef7b-3f9c-a753-bc7b3c994f83"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysxlogins"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/df29cf98-78b6-39c4-a32e-9243ac67a7d0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "getparentfolder (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5e6e274b-f9eb-31bc-a272-63d1b0fe5405"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( NTDaddy v1.9 ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c2430824-2492-36f1-ad23-cdf31d4ac554"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "settimeout (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7539ac42-e634-35dc-96a3-39da514f0fce"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "data: base64 (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/eb544bc1-a2a3-3a7e-a233-a1dbf1fcadcc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Neutrino DoS Tool"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a7a0a089-c400-3992-a8b9-6276da770ca3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ syscat.dbauth (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d6c60d68-e146-330c-adc9-4f13e9a0f42a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ UTL_INADDR (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/646592b6-3338-31e4-8b52-5421f9df2f04"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"emailsiphon\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2ed13b28-0099-3a22-8071-df3d878db660"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"eCatch\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0ba3c1c4-f550-39e4-8a87-3a6fca462ba8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ononline (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4d07db3b-84dd-3821-b2e4-7b97029ee5ad"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' || 1=1 \" (Parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a11e34c6-b1cf-3546-9716-7da27ac11a70"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ dba_users"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/97990f61-3b5b-38ab-a9db-a8a24fa0fb44"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"delete from\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/29743d5d-8053-3d5c-baf7-2e6cf4ffad1e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /c99.php ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3a71ecae-7862-34df-bab7-e29be94433ab"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /.dump/ )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/72348aca-afd9-326b-99f1-90a2158e8305"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SATENCRYPT\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/acd3ed4a-366e-3d33-87ba-e83d09371d20"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmessage (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9952d8b7-df32-314a-b24b-d57ad0ec28d9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop table (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5848c5ed-9d9b-34bf-8eff-0fd85340e122"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url javascript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/003fd235-aedd-399a-8073-08bea7044be2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Session Fixation Attempt - 2 (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a51d9c32-1daf-3b5c-8bb6-98f362262b03"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "@import (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a20bf43c-355e-39e1-ab9b-2a1b8a914e8c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onTrackChange() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d5c514cf-1621-3a33-8408-df29a77cc53d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Listing (3)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3b94ce3b-8b74-301f-b190-be930121728b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"BigCliqueBOT\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bda5c7ba-f434-3c3c-8ad4-4dbe0a36e958"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( wiki_up/ )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/48f4611d-7785-362b-a2d5-17a55329f674"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DoS tool (killemall)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/06d9c1c2-ef4c-3943-a61f-aae2e32b2589"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( phpRemoteView ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/668692f5-4183-3cd4-909f-15830464cf40"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"or 1=1\" (1)  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f37ed7df-021d-37a6-8743-36a5056f27ad"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysremotelogins"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6246d446-19ec-3468-a38b-0c6ca9551389"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"UPDATE SET WHERE\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a5a467a9-cec6-3439-91f2-4a3598ac2a23"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ user_users (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d3b35473-a1f0-3abd-b6dc-418dced8766f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like ' + ' (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c0a350dc-65b6-3b05-b260-38548926f4a8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onhaschange (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6de13c6c-412b-3e49-9cd1-2bdeeb34c232"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ into outfile  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a41c701d-4c2d-3d3f-9c05-dce13a807001"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onResume() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/539584c7-b38d-34ef-a800-6b98ea670138"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ CHR() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d24ac961-8869-3cf5-ad78-365ed77f4d21"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ UTL_INADDR (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/79a0d9b1-6ae9-3ae0-8e99-3841b3f70bc4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"chinaclaw\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/db3be287-594d-3f4f-bad8-94c02c9d2257"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysfilegroups"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9f6edf92-4f4f-3f49-8570-b184c21b5b37"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ v$datafile (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/baf5e39f-dad6-381e-ba82-12fc7f7c906e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like (1) \"' and 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0ad6bb58-822c-3f79-a8ac-f53a31788bb2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onafterscriptexecute (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f816ba6b-2299-3c7d-9440-21b1bb3375be"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".old (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b16772b6-f0dc-3c09-ac01-90379dd4da02"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onEnd() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/36b22da0-1e80-38ba-92e8-db95144f5238"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style list-style-image:url (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e734bbd7-e91e-332b-b6b6-da3737b2c4c3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ msysaces"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a2f67c2c-840b-37ef-88f6-b36e083fcc90"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onhaschange (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/42d4456e-03c3-3e4a-bab7-83d708148dfd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ImageMagick shell command execution in MVG or External Request [fill url(]"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bee09a4c-e1d8-3c05-af76-f36f0d3e2067"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' || 1=1 \" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1c79aaf0-a715-3a43-baf4-f82a905924b4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "FSCommand() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b4d083e0-144d-3ad8-b337-23b697cdc9cb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"node()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d7c7eb2f-73e5-3f36-b42e-9255a2fc3f6c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "seekSegmentTime() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ea6ef516-f004-352e-9775-fccf86756673"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onEnd() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/16b79a5c-4736-369e-857f-3e6881df69fc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"eo browse\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6047bc17-9b4e-3d93-bc8b-3a2241d76a16"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onDrop() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/54f07e8a-fb5a-3fd3-90f2-c8dfbdcdf944"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Jorgee)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8e0037ce-bb5a-3ce8-adb4-df5f0c726de3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onpopstate (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a2d06ae8-a65b-3b85-a820-8782f7b96ed4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ information_tables (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7e26991e-8766-3d91-881b-4c60072766a3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"if() benchmark\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/773b3654-f025-3ec9-9ddf-5ce718036424"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Non-standard Transfer-Encoding header value"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ce7e43c2-41ba-3c65-ad84-0d3b158d2b96"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Injection: commit; (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/07c4f5cb-6bca-3a96-913c-2ff33406722f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( CGI-Telnet ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e46fd86e-5cc8-31ec-b1c2-44014f40e833"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href vbscript (URI) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/19f15f50-9ed4-3a70-9d7a-71f7cc0f4917"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ImageMagick arbitrary file move (msl)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/edd5a0a9-bcce-3fd8-a302-2788ca196eae"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".fromcharcode (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8e2c7cf9-f332-3163-9b8c-bd9bbe63b685"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "LDAP injection attempt ( cn )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/090f757c-d1bf-31e9-a317-eebf2d947c1c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "new DOMParser (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ecae4e68-fcd8-327d-b512-a511ea124b38"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "img tag: src/dynsrc (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/49f2ec43-e810-3415-a97d-e1153dbb6096"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ waitfor time"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e44175c9-53df-3cae-bc38-09979a0d2ad0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onplaying (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ecaaec04-1d6e-3e7b-94b4-61da79cd6ed0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onRepeat() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/957ede28-1142-3622-979c-ae353b036089"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ REPLACE VALUES (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/96f9a594-e625-3346-bf65-44a581ab0826"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".open (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4fb4e8e0-5154-3066-b0a4-b77aaf0fa90f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript obfuscation (JSF) (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2b4a027b-e1ae-3b2d-a116-74a4f79537dc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"lwp\" (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b42afd38-9c3e-3850-9e50-bde4843f445f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "window.document (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/97910226-13e8-3437-b93d-24f834c432bb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href ecmascript (URI) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2f6181ad-5215-39b1-9ab2-c6abd81f775c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Hibernate SQLGrammarException Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fb0f97ba-1600-3824-b3a0-a57147a17222"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( PHVayv ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/28baae96-3455-3124-9a69-2af4dce87f3b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ current_timestamp() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5350c907-ea72-3313-bbe9-2da2179ea5fc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( IP HACK TEAM ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5c4b2f74-286c-390b-b9ee-50aa60a53770"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript buffer overflow attempt 4"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b8575855-4f5e-3b4b-9d13-66a82c39b69c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "getFromURL() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/49d3edf6-51d9-325f-9875-3f32f0a98989"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onbeforeupdate (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cd170af0-434f-371a-a9d4-0d507303e842"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = text / script (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/095b8ef7-d46f-30e8-817c-099b172c4803"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( metis )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d6bf4caf-43a8-398f-bcd0-e62e814dbff0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (WordPress)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7916880f-72b1-3657-b261-32f9d55695fa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href shell (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/21409b6b-8aa4-3d98-b57b-9e34def1f739"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ODBC Invalid Argument Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1aad33b8-b796-3492-a1d0-a5bbbefb03da"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onURLFlip() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a24d15b6-11d8-3918-8419-053746e2c342"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style: background-image (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2efb5e52-209b-307a-826b-f0fe2eaf5277"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"Interbase SQL invalidation\" Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/baa33368-4227-3dd5-8051-539dde9200c8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src shell (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ffd2916c-f225-3709-81dd-cc021e4b20b6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onresize (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0868994f-0042-3fe3-accf-6b2164211795"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select to_char"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bb685fe2-df65-3468-b9af-9240c3c58891"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onOutOfSync() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/83828051-33c4-3708-abf2-2369a87ab0ab"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url ecmascript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4442ba2d-409d-396c-896f-6e6cf11ec457"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onkeypress (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d39a71d7-bbc9-3015-9ab0-a5591929f116"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( bilbo )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d03bd66c-6ccb-3992-943f-4d18df6ec27e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ 'dbo'"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dce12e02-5bca-3e1a-a2d5-1ab8655002e1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "img tag: src/dynsrc (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e2ce4089-3852-31b5-ac9d-67ee51186423"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ cast("
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e1dccc44-ee4f-384a-91db-26b68d765fde"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"' && 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3ba41f5a-1bf6-3cc0-8e9c-283c6c79c22c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (Java)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b375e320-9fd0-34ee-bc63-9253c4da49de"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' && 1=1 \" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/69d994b0-653d-38f3-a997-1fa5399d923f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "LDAP injection attempt ( homedirectory )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bea7e3fc-899c-3702-a2b4-657bb743a5b8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "OpenAsTextStream() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/60f0a46a-9966-3c4c-a9d9-d7a18d71e05b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"if(Expression,value,value)\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b804eef8-6452-3765-bdcd-b118c7ec8fa4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: binding (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6c56e65-750a-3303-96f2-2ced97723ae0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create trigger (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e32e3b13-f7ce-3207-ac6c-9749a838ed9f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Nessus ) - 4"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8f79ce37-1b6a-3b96-ba3d-6a28a15539ec"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ insert into (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b84bad71-15f9-3b42-840b-e440aa1cd375"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"translate()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c9ae5f6b-8bef-3464-a8ff-1339ef26ee86"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sys.user$ (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4e5edc4a-1978-3a00-a97f-56a9ebfaede5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ BENCHMARK (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ecd558b6-fea2-3f91-8908-cbc4c68e957d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onPause() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c30fa0e1-b491-3cc5-a077-b6d5027bb2ad"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"cast (\"  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4b6a5ff0-1880-32ac-9b1e-e0536315dd98"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (32)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7eaa80aa-59c3-3997-a91c-b544a84a146f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"pcbrowser\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5908c64d-7e30-3f95-879d-8b2de483d547"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".bak (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e87a6e59-5673-3cb6-ba32-9bc868e94ee0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "LDAP injection attempt (CN in Distinguished Name)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/22b5340e-c70e-3fa9-b496-53e4b93cf934"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malformed US-ASCII - script tags (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8576a8d0-93ce-34c6-bc9b-bc90b6536bdc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<EMBED code (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2dcd074b-47de-3203-be11-bf54901d4d86"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( nsauditor )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/030c1360-acd4-3887-9849-62be1ad0751a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Perl source code leakage (1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a8d6e3fc-b6e6-3228-a66c-85b381df839f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SUBSELECT RETURNS\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d937e940-3fac-3245-a908-ccae24804ea9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".innerhtml (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/642c3973-c79e-370d-b665-8dc37e8044ac"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src http: (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a59f0c60-770f-39f5-b27d-5096f299ec6f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ UTL_HTTP (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b13006ae-cf16-3de4-bf47-379a36665b96"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onunload (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a593e2a5-ef72-3ded-9524-0b4f8f2f3982"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ REVOKE FROM (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/258264e5-fad6-333c-a7e5-6771e278a5f3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "button tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/189af5ed-9096-3db0-8661-139fc3fef917"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".location (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ccaba775-0263-3c22-a238-1b0cc051d84b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onRow...() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e9df2f2a-e71e-3d3e-8c2d-d25562c1c0de"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"schema-element()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c83573ee-aa22-3f2d-ac21-f18c6357a97c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ASP ADODB Record Deleted Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b2315ba0-dfd7-3f82-bb68-de2ff1d32be3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"emailharvest\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bf12ce4f-f5c1-3d4b-804b-dfc491ec6602"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ msysqueries"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/38ff8962-0262-3102-9790-8260f9175744"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"NICErsPRO\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3abaadaa-c08e-3606-8d0b-4ac94914ca95"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"or TRUE\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/24537765-599f-337c-ac5c-c9d4dc2d26a4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"ecollector\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1867c33d-bc1c-326e-ad51-0149a5b18eb2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \" and 1=1 (6) (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5182040e-ca61-3510-b2bd-1bd3f59ef04d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ user_tables"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/10adafa6-3dc4-3fe7-969b-e27dfaa668a5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "mocha (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c3b131d8-4979-39f5-9031-a3f0bf0af8b5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "[window] (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/73824ee8-9c83-33de-9e52-0be9f7c09119"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<OBJECT data (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4bd9e01f-5f81-3e80-a0b2-59d7179c81e9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (urllib)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f34ac146-8f6c-3965-b5fc-d10d5e808097"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"athens\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cdf181ea-320f-3e8c-bb06-3e4cac1016a2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".open (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/39faf02e-a1cb-3bed-adc1-8d8372139b33"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"ODBC invalidation\" Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/da46bcb4-743e-3a14-8752-431071a082df"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop procedure (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d3aba959-403c-3e87-9e7c-0a044abe4e9f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"attache\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f023b135-c4af-3f31-a89c-b0ed688d0e72"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( n-stealth ) - 2"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/90cf57ab-3f3a-30fb-be04-e3d3fc6fa339"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ exec()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cd12d973-3552-3c62-bc9c-da6e43359447"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SYS.USER_TRIGGERS\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bbde72da-4d4b-34c2-83e8-b90d621261ec"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "bgsound tag (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7f629c84-c6ab-32c5-b59f-4608689468da"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic test dir access (/test/)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/35d70b98-8028-37b9-88ff-785be229f78c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onTimeError() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5b47afce-ba82-370f-bac3-8080a2554ee6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<MATH href (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4d32ce31-b30a-3f27-945c-13ad6809c64e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (ContentSmartz)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/32cd7154-fa4d-3485-8d2c-8339ef85146a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Server Not Found ASP.NET Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c8e4d7d7-8755-384b-9eab-555569b75886"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"ProWebWalker\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ae026347-73b0-3370-babb-da012a4e63a8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url vbscript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/50080dc8-ca9a-3c84-b92e-55960d1b8399"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"end-quote UNION\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/10e026ff-fdc4-3a45-96b0-7d2a88cfa2c8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Session Fixation Attempt - 2 (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/678bb6f2-7492-3f53-bfed-8d44642d7e0d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ atttypid"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/717cfa09-c4de-39f5-8d1b-b56bd9e2202e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onvolumechange (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b63a2c39-baf1-3cee-a1b7-4f6d1c09e978"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onRepeat() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/030a8a12-8345-3874-be0c-2f488fcc1a7f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ exec() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8ec43bc7-e174-3b35-943a-9c70de3915bb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"Amiga-AWeb\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/eef84b8b-9415-3ff6-b603-51000cd6c596"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "bgsound tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/159e7dad-5e84-3c56-9bbf-1fafca9eeec1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onSeek() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8459d858-aa0e-3970-913c-4f10af351490"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ dbms_java (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6f74574f-5a74-39b0-9c33-ef6dc133db28"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"sys.user_views\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/867dda82-3e5b-335a-b17f-960d9dea5772"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic buffer overflow attempt 28"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1fb3825c-3d47-3b03-90de-01dd5855a3a6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "xml tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/29f127fe-df98-3316-b299-5eb2946c39e6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"' || 1 --\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ae34f195-beb4-3124-8083-4a1c3834be04"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"load_file()\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7f911a00-9e33-3b63-b96d-0cca03dc68bb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"delete from\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1e8a007e-7662-35c9-8e94-a28bccf871b9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onstalled (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ef1b1c40-136e-3ccb-88a8-f29a2bf4d2e4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe httprint ( Mozilla/4.0 (httprint) )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/26487756-797c-3cf1-840a-2623a318468c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ current_timestamp()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/517dbcce-387d-3e66-9ccc-c4dfd269d70c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ information_tables (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1951384e-5c5d-3fd1-b583-0f499bb7436f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "[window] (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0da8ffee-72ca-3ed3-84c8-e6c48fd23ca5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (3)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/860bd055-316d-347e-a9cf-2f0b5b5b26d2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sql_variant (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d6797051-1d47-38e0-9e32-7329cf9fa3a8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src http: (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/24be3e2a-1b3a-3c8a-98f0-56e36744552c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"sys.user_views\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a7ad31ff-fc3a-325a-98ee-d56e59157611"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( iMHaBiRLiGi PhpFtp ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d0bd05c0-3ced-362f-b8e4-e4a0f9660b57"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.cookie (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aba9c3ec-5fad-3bdd-938a-448ef4c3e3f4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SqlException Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/af1cf74b-27a5-32ce-9849-c7aa561e56ff"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop function (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e15009f8-6bf7-3a87-b41d-48c50d2211b7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/40c4eaf9-b50a-32c2-a04a-f5e8f01003f7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Zope Information Leakage"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8ba1cedc-7084-3cad-93eb-db91745787a3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"mailto:craftbot@yahoo.com\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a8f38639-8ef8-3473-bc85-f083c5c4b646"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b240d4ae-f605-32b5-9a8a-c356104e256f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "urn() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/96418838-c8c0-3e3b-b7cd-500d3d175927"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) ipsec.secrets access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/949a87c8-b8a3-36ae-96c9-9ca8c524b289"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOMParser (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/570a6f6a-ae56-33b8-8999-a45063684a54"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Zollard)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/62e28157-941e-3532-b6da-7b98d969a923"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "unescape() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fd5bb861-bb03-3781-99a9-52f06c70e1b5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onloadstart (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/194f8215-27c8-387a-9405-a0c4a567ffc0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "eval; (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8731d99a-b8e2-36dc-a2eb-1ca5c097af7c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' || 1=1 \" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2933e468-376d-31ee-8621-ef313cdf24d5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_availablemedia"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e7d6f87b-3efb-3ad0-9b2a-fbf58c2c4096"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( NV32ts )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e3b450b8-03f6-319f-928a-e355316359d5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onwaiting (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6e8e5955-516d-317f-8723-9f4bd7bf771b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (ESurf15a)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a7a2fe10-b250-3811-a9e4-6967a5fd15d6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".send (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3220ddab-eb9a-3e4e-8bcd-a9341571eb2d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_ntsec"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4dd70bec-e4fc-3dff-8885-8b9d946e33fa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmouse... (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b26c6cc7-01e1-32c9-8d73-cffe28dbfb86"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"BACKUP DATABASE\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0d3a7f26-1202-353d-b3fe-8cc39c14ae9e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ truncate table (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5bcbfbd9-236c-3fa3-9e5d-ba23a9e10599"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8d031fb1-91f2-3044-a957-ebfafbc4ff0f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"SAFEXPLORER TL\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1b5b1b0f-1a1d-3edb-ba02-e50493d3f0c5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ atttypid (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aea21f23-7eda-3401-b286-b2b3b0f6950a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onBounce() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1c9640d3-dea7-3417-9b4d-3afa6a8afa12"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \"/..%c0%af\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c7cc8154-af83-3b0e-a3b0-3d549ef285d8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.form (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aea295fd-b946-3174-b78b-f0921d0ea09e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (GT::WWW)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/29cf29d2-ff1f-378d-b767-f08c537396ed"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ print @@"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1673d6dc-2a81-39cd-8e48-5fc3d5761c46"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) DB2 error"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/60149528-e306-3253-8596-e2ad489b101b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create database"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8299de10-83b7-3f53-9820-b7658c71ccd2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Injection: commit; (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/255a83d1-2170-316a-b115-f47f1a2464d0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Netsparker )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2859c7bb-33eb-3d31-94ea-6fa4d1db4436"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href javascript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e4b7830c-ae00-35ab-9dbb-92013b58c8f9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) File Upload Manager Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f9fd9f97-6c7f-3c2b-8762-bd03f82f23ad"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "window.document (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d10861a7-46a8-3c25-a4cc-0c0f92164d43"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"dbm invalidation\" Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3ce590c3-5bc1-34b3-a95b-3f0d4440c5c0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_regenumvalues"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f97ffcae-e3cf-3dfd-9bc0-d86da6e76c3a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"sleep()\" (2) (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/939cd143-8370-3869-9f58-9d7c81a5d8ca"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".location (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7f6c4745-7002-3343-a90a-9d553ad052a1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (6)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7569a472-de31-3d05-ace5-d0fbb03ee952"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "OpenAsTextStream() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/533ecb2b-8382-3552-8ec5-cf2c5859abde"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Samba Web Administration Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f12fe532-29c4-3166-a461-07c30d37466e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (China Local Browse)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/97edf519-e921-3170-b256-01f563f21d85"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ instr() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dd8ee44a-d730-3762-9cfd-436acb368cb4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create procedure (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c2928927-fd55-3ee8-8bc2-93070152a232"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onhashchange (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7d107917-34c5-37a6-83bb-f52611a1ab1d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"custo\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7c8959c0-933e-3fef-b5b5-438d09c67155"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_execresultset"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/188e5ec9-7dd3-37e8-abea-0ea828ae74cb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script target (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d0b56127-411c-3d04-a02d-66289d314789"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( r57shell ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/326837ac-1b3c-3c3c-bace-047daf86a47a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript buffer overflow attempt 1 (Response)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1504743f-e5e7-3d8b-8072-62326c274d3b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /cmd.dat )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4a7636b2-83b0-3534-a9a2-45b2e228660c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ column_id"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ff2c77a0-7b8d-34ad-a67e-b0b3fb8bf82b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT CONCAT()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5fa94cd6-932c-3303-9db1-a73a0f475e29"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_regwrite"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/96172a8d-fe87-309c-bebf-a187b9d8f937"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onReverse() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2f69e9ea-d409-39f0-8872-65fc7c86503a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onSyncRestored() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c162cc8a-a074-3fdc-9dbf-bd93777d4eb0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) MRTG statistics Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cfef2a79-43fc-3c00-87ac-fcec2e7a59cc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "decodeURIcomponent() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a58417ad-5c77-3e69-a257-f70dd9c83782"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (MFC_Tear_Sample)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/85fcdcc0-56eb-3623-b841-26f98a43be98"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ benchmark()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4f354237-a1be-3f4d-8d77-06f0a4238b6e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Nessus ) - 2"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ee3ef3e5-472b-34b7-9f26-21c41e683285"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".FileSystemObject (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/42c29b6b-3f64-34df-b10c-302d57df8f22"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onload (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bb49468e-4fb7-33e3-b9b3-3025af6f749a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ ATTACH DATABASE (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c98ecdb3-aff2-3890-9bff-83c85e1d67aa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onselect... (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ef9ee4f5-ba63-397d-8907-1fd2cd400bf6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (30)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a942fec3-8052-32dd-a5c6-98e725fd816d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ pg_attribute (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dfe63577-a9ce-38ee-afbd-c00a92d45b43"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic buffer overflow attempt 29"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/45dbb053-dcf0-385e-87ed-0b9feeaa991c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"GameBoy, Powered by Nintendo\" fake UA"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dcc6095e-e3c7-32c3-8ea7-52196a1276af"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onresize (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6e02ed99-4c9a-3fb0-b870-163d3a1f5092"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".execscript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8ff8cfbc-bd1e-382b-8e2a-f2cc8c86e929"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onsubmit (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2aab3711-b292-3d2d-9c95-fbd481896bc2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onActivate() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d524afb4-e662-3b9a-a057-97210236a8e5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 3 (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/debaf294-9588-3582-a061-41e8d299022a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url shell (URI) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1b4eddb4-a8c9-32aa-b750-1f5e204350e4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Number Out of Range SQL Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/22afbc8b-e247-3e24-863e-c37b8dc011e9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript obfuscation (JSF) (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d9304530-30b0-37de-8d60-d2c995407ac7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ rownum"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7588e520-6c98-3a26-8b1c-6b45cefef377"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmove... (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8c34dd95-f0f0-3677-a673-661cf944fa9f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href ecmascript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9528698a-164c-337e-944d-316dc696eb0c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT IF()\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e123b538-fb43-3292-bc73-d619ef8ec8b4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"FileMakerPro Query Invalidation\" Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/01b32bea-d0c0-3415-baed-2ba2398f0ee3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "input tag: dynsrc (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/597241f2-c90b-3c94-ad98-702a245fffb7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"emailcollect\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a5b525e1-16c3-3b3e-94c9-869bcb2052b9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src vbscript (URI) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3e6236b2-6fe6-38fe-86ea-a06ceb3cfc84"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "[document] (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e294daa0-46bc-3b64-9f9e-05b717941e8b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ integer field UNION (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2ea5bd86-e443-3510-8f15-ac5ad104b737"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oncanplay (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/13caaef5-6955-3c74-93be-f0c2107365b9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"Runtime.getRuntime()\" execution attempt"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bdcd1044-afcb-300e-9af3-d48eea6ba0da"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"agdm79@mail.ru\" spam bot"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fbb98998-7fc5-36c4-b4c7-b0326f2efcc2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe (Nessus User-Agent)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/37625007-fe1c-3438-afb9-925f6d2a4abd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"Windows-Update-Agent\" fake UA"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0f041939-bcc2-3ff3-9d65-317e73553d26"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 1 (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f25cb459-8bc0-33ef-895f-fada11960884"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"adsarobot\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5e141a20-3609-3a01-aa22-e9baa78675a8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 1 (headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2e6948d9-e95d-336c-8521-dc0728bd189f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CreateTextFile() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/abe68512-8c6c-37da-9e11-01f96c1b91a2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( NTDaddy v1.9 ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0318bf06-cfa0-38d2-aef7-c40b81503c9d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onplay (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/be16f782-1218-38c8-94f6-3be60b528f13"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onResume() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5fbfd176-027c-3875-8115-77606bebdfeb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( WwW.SaNaLTeRoR.OrG ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/55ef0a51-d198-3b54-8ffa-e6313f00dd17"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onDrop() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e347081d-c85f-32aa-a5d1-3db1fb18ee8e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"select 0x\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4b51260b-c630-3fac-af96-9e2637acd969"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"Microsoft-WebDAV-MiniRedir\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9090cdd0-11ea-3669-b8ff-2a83f90cacc3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"following-sibling\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a5fd7185-fb0f-341e-8daa-19189f424d6a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "cgi-bin/php access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9ec15e41-0e65-3ff3-b834-58f7055bba03"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "MsgBox() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0305ba2c-4e97-3df7-a5c1-34b79626b266"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onMedia...() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/20b40b1b-b3ac-3597-a259-9ac73b1365a4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ user_tables (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fb7adfc4-0355-319d-80ea-e1cf4e712aeb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"fantomCrew Browser\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3640d43a-07de-3754-97f1-3fbf36aea727"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"site snitch\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a5a2741f-6d58-3ac9-84fe-1d2cb8a3d079"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "FRAMESET tag (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3be9de6a-4049-3e98-9a3b-e186aa834b65"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"or 1=1\" (1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/46c98662-6603-3bee-ad25-fbe9f49b82fe"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (DSurf15a)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9b6cd929-318c-332b-b372-8d559d03f0c2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "bad HTTP/1.1 request, Potentially worm attack"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4c719112-5374-38de-b24d-5b9e332455ae"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /scan1.0.scan/ )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5ad64ed4-a26e-32a3-bb19-172d7855754a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create table"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2bbc5fba-ca99-3664-a0b7-747ee22923de"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ group by having (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ff5c2393-194b-3e27-981a-6ff21b552d05"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sp_addextendedproc"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/225ca768-f374-3414-962e-1dd70d51efc1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"sys.all_tables\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/06270a5c-d373-3707-9aee-016f351110b2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onpagehide (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8db982dd-480c-336f-9ff2-104cddfa69de"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Bork-edition)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e15415b1-601d-30b7-b642-cfde4c44e3d3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"' /*\" (SQL comment) (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e9a64470-fe4b-3e4b-abe2-da28b0ead2c4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ CHR()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/857519a5-db65-33c8-83c7-7c7659f5c046"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CreateTextFile() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/05d1eca8-df1b-3897-831e-92562f8d51fa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"reverse()\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cc06aa6d-428d-3971-9c06-499a2e419b4f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<EMBED code (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0da5b52d-4b73-3730-aebc-11adbd5ad494"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<EMBED SRC (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3edb24b7-88ab-3c5f-9e79-4574a9e6da72"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"sys.all_tables\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7b89e27b-08f8-3c67-a28d-a2a7c279511e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "link tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5120d385-dbc3-3b9d-852c-183d8ec57d9b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sys.user$ (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e035468f-53f0-351f-bb77-3aafe3b05f79"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Wells Search II)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d16f84cd-edf3-3da0-b6f3-6640625a5d89"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "history.replaceState() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e84c818a-ce48-3714-a0ca-8828fbd41169"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sp_sqlexec"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5346516e-1820-3810-9609-f4d9e445662e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.createElement (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9a32d70c-cb49-3b20-84e2-2c9d1a1ce6f1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Form injection (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5bec7f24-880b-3c5a-bb12-5eb48d4a0051"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "whisker HEAD/./"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/84f3cfb2-6eea-3991-8b50-2f926f9affdd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onbeforeupdate (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/65ccf006-0950-3c76-a87e-3f44cbefae9a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt (parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3bbf17da-ae32-366d-89f8-3958b4c26540"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"comment()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ca987378-cb9d-3bc2-b947-a8d2707cd346"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web-Server sample dir access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f3f2aa79-1a64-3d6a-9610-eb391a209a57"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTTP Response Splitting (4)(Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bcc48048-2a4d-3620-89f5-020e260ce7f2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 1 (parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7d6cecda-3083-3973-a15d-8cd31f1b3a5c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oncanplay (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/86e413f1-8b8c-3a19-92f8-866c99e4ddb9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url shell (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f6c4ff78-6e97-3a1b-9aae-c1bbfe644f1e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT TRANSLATE\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5144cd66-3a20-36ba-adc7-23313a9b5847"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Comments (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ea627155-a64a-347c-940e-f9da54a23faa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "httpoxy CGI vulnerability - HTTP_PROXY"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ac4fc050-57cf-3fe2-a689-dbe66741646f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ SQLIVULN_CUR_USR"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/df24f4dd-499c-3232-93cb-525cf10eeae7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"attribute()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a31447e4-5b97-35fd-b1d6-c8d4c0e99209"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ openquery"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/be11d55d-e2ca-3721-ba66-4e1c7fe40c76"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 2 (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f4b44832-f918-3a7f-ada4-2adf1b754a9e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onStart() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5123c68d-1ee4-3b8f-bb85-bbffd85a2554"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onselect... (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2ac6e904-eee5-34ee-ad9e-2172bce6ed8e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"and FALSE\"</"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3c9920ce-5633-3053-bce4-a3adc55ed509"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"pavuk\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/28e18199-b47e-3624-9b24-7fe98de3620d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /sikat.txt )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7c192434-8090-3880-a1e1-15d071314910"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( iMHaBiRLiGi PhpFtp ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/06fbaab5-a14b-3de4-879d-dfb4106929f6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url javascript (URI) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e36bfc60-68d7-326c-9350-2974111e2555"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web-Server Administrator dir access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/71ea9d2b-3146-36dc-b593-0b1d7c6f4708"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (URI::Fetch)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8f17d45d-3c0f-3acf-8580-c08a93e8d9c4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malformed US-ASCII - script tags (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6b477643-c5c8-3f50-96d6-845eca61e6d3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"delete from\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c722f647-041e-30e5-88a6-7c3b999df642"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style: background-image (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/429e2d7c-7d0f-3499-857b-649db3f75fc1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "/Admin_files access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/62a43f61-c4f1-3016-a6fe-619c2fdb550d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"psurf\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7ce572af-5e47-3155-b4aa-ab66a1f2ea5c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onResume() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b1b17cc2-63dc-3ba1-84af-0e7187173318"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href vbscript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/109094a2-6eda-38ae-81c0-aa7dc0a06e42"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( c99shell ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b7aa6d20-fce4-3035-ba56-5b66972dff9d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onBegin() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cd138e7c-7907-3607-9ff7-2875312c89f2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ v$database (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b4c2c621-0b99-334a-86c5-394fde17019f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".ShellExecute (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0fb4660d-a079-386e-bd7e-b2a92e8cc68c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onclick (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/99e71460-03ac-3d63-8019-f2a8a0fffe7c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".responseBody (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3d78f49e-0221-3a8d-9ee4-30d73c578859"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic \"<style>\" tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2c2dd073-e8a0-3c5a-86e8-f2f368a7de3b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTTP Response Splitting (3)(Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8948e587-747b-3ec3-a3b7-474bf22c2ebc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0daa744f-70f6-3418-b97c-8077e9e9620f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_makecab"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aaa6ac6c-192e-30bc-8591-b87606e3cc60"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ BENCHMARK (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1e2e85ba-7f33-3066-b620-bb879af65bd6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Morzilla )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5d1ed3f1-71d6-34b4-bc0e-8a5c775fd18e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( anggands. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/38cabda1-a1ca-30a8-aa85-5c52ffa3f021"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "createtextrange (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c08e8cd4-dafb-3e1a-88fe-eab0ec5474b0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( ProxyStrike )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b5c75e23-e814-321e-99d4-7d4d8a0e3590"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ alter database (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7a83d6f9-da52-3468-b9c3-295df2d27814"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_cmdshell"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7b55c9e9-d2fa-3e57-bab6-dae6e3791448"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "button tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/24d0625e-1c90-39d2-a02c-cd81638e1354"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"autoemailspider\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c14ecefc-9b6e-3193-b504-6b62b2ca12ed"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "touchstart (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/88e64ec6-e3e5-3392-9b1f-1438bc315b55"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"ALTER USER SET PASSWORD\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/264fbfe3-89c6-3e90-ae86-12e83398ec31"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oninput (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ee10ee16-ef75-3be2-bf8e-c77e42331e08"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (4)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d6a3ab18-f85e-31f0-9f74-509e571bd9f4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"UPDATE SET\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3e2a0a19-4608-30c9-8e1c-f8b6e4f3143e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src javascript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/94b9d83e-d2fb-3917-b51d-ce9f77334e39"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onContextMenu() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/63751563-712c-3d18-8fab-6c33daff3fe2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onpageshow (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f6df90e0-04cb-3049-8c19-fde70682056f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onvolumechange (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7638774c-8f15-3e33-8fa9-1ce674fbbf50"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ syslogin (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ca7cbb5f-665c-3f81-9e2d-c552900ea6ed"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( mozilla/4.0 (compatible) )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3fea0c48-916e-365a-b859-37bd23803340"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' OR 1 IN ( \" (Parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/761c319d-8da9-3b15-9f33-9ac4ec73d252"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "execute() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/55c31035-9528-3fca-b7a6-4cd7a75f9fe1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Statistics Software Information Leakage (3)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f48e569d-680b-33c3-a081-80784e468426"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic buffer overflow attempt 27"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/065e9772-58c1-36e6-b1da-a1cb439213d0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"UNION SELECT\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/72e46ee2-2841-34b7-b1e5-f8887cf140ff"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onseeking (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4192c2b6-e4c2-3ac1-9c2b-60c3db0cb0b1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "window[] (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/21524f57-b8af-3837-8ee0-b2beb82112f9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onblur (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c914389b-d6c6-3f3d-ae9f-213c695e2a32"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src javascript (URI) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/995fbb29-31b4-3c15-a6d4-21a7d6efc59b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Temporary file (.$) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bae37cec-18e9-3e16-91ec-869087fb46b3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ REVOKE FROM"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b5683254-31f9-3d93-be1e-303bf59a64a2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTTP Headers Injection (7)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c3da7c9e-80e0-37cc-89c5-7dfac44487f5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ tbcreator"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/03e20d87-4e2c-3cdb-87d2-6587e32519aa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ondurationchange (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/29971479-c4e4-3b5b-8617-621e158a2044"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop procedure"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f34e82ea-bc88-3341-ba26-557b4d35410a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (23)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/87444642-425f-3bbc-aa34-70aea76dc6a2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<MATH href (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b327056b-51b1-30bd-82e5-c48a2be48c34"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Headers)(3)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f3b86a7f-4c29-35ed-bc1b-4cf6f71a5c45"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src shell (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fe0a36bc-e32d-36f0-ac75-e93c461f558e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"sys.tab\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/815b2796-9f00-3316-867e-d8b12a8605a6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (ISC Systems iRc Search 2.1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b9d0d87f-0515-3176-978a-bd727c3ca468"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ODBC Syntax Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/783659df-74e4-31f2-a311-b4a0a3f01945"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"namespace-uri()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5c760455-7911-36ad-947a-95b006c1105a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onPropertyChange() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9cb15cc4-51e3-3cee-ac61-dd85c05e7548"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' && 1=1 \" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3d6a1a4d-b60d-3026-b5be-52ba58be4fbb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src javascript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/711cb53d-3f89-35f8-9b67-db868b02dca4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "w00tw00t probe request"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5b5f0193-ce94-35b1-a198-d24a60664918"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e51d865a-c1d4-3bc3-8834-6e0fc9edd5e4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /nstview.php ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dd0cb3b8-9a7f-3b6c-a222-e222d1a0cf25"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1cd5ebdc-d71f-396f-957a-c85417b7cf0b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onfocus... (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/00c6485a-d992-3827-bd2d-5c0fefccc71c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".documentElement (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c399b591-bf07-3325-9157-891634f2e5d8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ column_name"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/98320422-937e-3054-b49f-8b2073b2b31f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "STYLE tag: binding (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6759e110-ec06-3d44-af56-f0772c57e21f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onStart() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e4d6c896-3dd7-3888-8a02-4ced3c7f9209"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "/intranet access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/98715de8-654d-366d-85d4-9089dfa75494"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Injection: commit; (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fe83dfe7-e2b4-32b4-a8b3-b20c26b00007"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onclick (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e2645cec-1c52-3f1d-b76a-bf9940cb1248"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onloadedmetadata (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/70f1ce10-e85f-398c-aa1c-4c7624eb25eb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url vbscript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c5f78d30-e6de-3ab9-8694-e70047a6eab8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: expression (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cb00fad2-3455-38d5-954a-e6271c90145d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"grub crawler\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d40c684d-84d0-31df-b4e6-4cd1b157c715"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onafterscriptexecute (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/613a6b49-36a8-3c65-b48f-43dd6375e32d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oninvalid (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7389335f-38be-3d79-8b49-5f1f749849d2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "STYLE tag: binding (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f6c8b4f5-0b7a-3157-808a-d7049d95a663"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "-moz-binding (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0a02051a-2a8c-3b54-89c4-872a2ed83221"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"UNION SELECT\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/919d3053-184f-3752-8187-7eedcbb7c643"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( c99 1 ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7e654c50-9f8e-3a8c-b7c1-82b81e4ed059"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "toString (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4b35105a-bf0e-351a-9f8e-fb18684c4e02"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onEnd() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/605a6751-a2ba-312e-bb38-92f7a397d5d0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"WebBandit\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/41f7ab4f-2a98-3020-b8d1-a5a10836ecb3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"parent\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2eb080b1-a3da-38bf-8325-7c22ffb9a7ef"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (25)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ae0dfbb6-d7e0-3fc9-b7fc-cbb555be3d63"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src vbscript (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a9db9105-c6d7-3c33-a8ed-95bbf9d420a8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "settimeout (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e671a26a-9bf2-3f11-ad84-cd37802fda2a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url vbscript (URI) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/faa7342b-86a0-3bd2-903d-efdca397bb3d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Parameter) (3)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ca43c08b-f171-32f4-9a8a-9aae0a0b6eab"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) SnortSnarf Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1efbac6c-5627-3f71-a2a4-af7a12720535"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (10)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/04ead1e8-7817-3321-b786-c3eb3f7448b9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"or 1=1\" (5) (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/89e4d9b3-275b-3e8a-a469-45dc3ec6fc4a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Parameter) (5)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b633ae27-b42c-3411-b870-f1bc602df2eb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onabort (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aa482eaf-fc8e-3e2e-931f-72ef22af6ed7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sqlite_version (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7e56de0e-b146-3a9c-930d-d21b5754c5ac"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<EMBED SRC (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a8778672-5574-3cba-8fd1-d55629cd9182"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "/.svn directory access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/065caa58-9d39-38eb-b65a-fe7c3e9715ae"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (26)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5f7eb3d2-cc9e-3e77-9622-4d42b84fa281"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ user_password"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4ccfd08d-02a7-33a3-be7a-dfda6544853f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ exec() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/576b30b5-ed92-3173-b877-9347a16a5b74"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script tag end (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/31d88ddd-ff91-3dd0-bfe9-015fe6f58b5d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "data: base64 (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f95eca2d-b37a-3fdb-b654-f20f61fa5940"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (5)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2ea9c5ef-826d-3a39-ae0a-fc1f9891baf5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"CopyRightCheck\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5d29a0a1-1825-3beb-bbd7-e499d0d6d060"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".execscript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/12444fdc-11c6-3087-96cf-5abe3798789e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic buffer overflow attempt 1"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/145d2876-7852-38ba-bc4e-9913ca2a8e55"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Different Number of Columns Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c2156cdd-81cf-30e2-b5c7-368f3bc077a7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"oem_temp\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bb35dc31-1d66-32fc-a4ef-ab16afc76a89"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysobjects (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/09ff063a-60ff-337a-a251-0af78edb9afc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ mb_users"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d780f3cf-c892-3d73-9b1a-f46e89569117"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ws_ftp.ini access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a38d8772-3c46-3f88-880f-94f03bc4aaf2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "meta tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3bc9bbce-61d9-3f10-afe6-b6b4beeefee2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "eval() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/35757414-6e7d-3575-bf7b-0b34efbb27bf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onkeyup (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/048acba6-2cc8-30da-a14a-cd07fdb24826"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web-Server example dir access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9ac9f369-4b37-38e5-964e-ee69794c8e8b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sp_executesql"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/91a8717d-d49a-39de-a12b-2997a8d50939"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onDeactivate() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c38f1c4e-9559-303a-8189-9b3b45d36747"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<BASE HREF (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9c81b72d-6df6-3f5a-b536-c46ea8157fab"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT pg_sleep()\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f2ba6055-19d6-3982-9804-7390e3ddacb1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"Expression::Type=Expression\" (Parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ad0aceef-99de-3567-a33a-bb9d42c5f66f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "BeEF HTML detection (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7d902fe0-5b8b-3235-99ca-968f5c11dcd0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href shell (URI) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9e2327f3-d20c-38b5-8f57-ef1b8e18d223"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SA_FORWARD_TO\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/326294d8-c5c2-3c06-8ca7-e9a010ea1bfc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Suspicious \"test/testing\" file access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ade04868-e6d1-3bef-af7c-9d8696b54f54"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onshow (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1f61af5f-539f-3687-bc11-f2c69f1a03a9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onReset() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/88206f37-ec79-33f2-9a0b-6e9f756663cd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "link rel stylesheet href (Parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ff5cc6a6-0be3-372a-8bd9-688516f2a7ea"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: behavior (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a27a6e0f-5679-37bc-a817-88d07fdeb155"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onContextMenu() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/edf5b260-473c-3d1e-b763-10e7e5470ebb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ textpos() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/22505672-8f33-3885-b5f7-32c6efccc9b3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Escaping server-side escapes - single-quote (Value)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e9dc3ebd-5810-3618-8460-c73407bc22c1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onError...() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ae5f5384-6bcd-3099-aff9-a39bde645cfa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<![CDATA[ (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9a4df2f0-a3c5-3a02-bf1f-35dc63e23621"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".SaveToFile (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5e3f530b-6ed1-365a-af5c-842c30c2391f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop trigger (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cab8c48b-b490-3652-9bfd-630889aec8ec"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"CREATE USER SET PASSWORD\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0f990037-5ce7-3cdb-bbed-30601a906960"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onSyncRestored() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fcdfae9b-dde2-3147-bd83-7002f5bbe06c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ attnotnull (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c1db9835-307e-39f4-8ebe-9280ec52dbaa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (HTTP::Lite)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/84ce27b8-744c-3679-bfa8-bc4a87186727"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( btn_lists. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/152bcf94-4ab3-3f8b-b524-4648f83249e0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"/config/\" access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f3c55f67-a60b-3dd1-9a51-0fcbd5101930"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( n-stealth ) - 3"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6da3715-7822-3717-88cc-4b35d2b7fbd1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like ' or 1=1 (6) (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/78d73471-713b-3ef2-997b-ab8f1022dcd0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onScroll() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2dc12720-d3d1-354f-9faf-45150aa3c95a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"text()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2301f550-3e4b-3ed4-8754-b6f625ae0f5f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ pg_class (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5965ab66-f278-3d24-94e9-3739f86019cc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "activexobject (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a1804cc7-647e-3727-bdb1-5a0ae8f9e165"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".createDocument (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/51984c78-ad06-3e3a-beaf-e392950dd71d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src vbscript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/752cf759-5ec1-34cb-8b70-26c4e545e044"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Injection: End Transaction (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d1f3d8b0-2f36-3879-96dd-cff3856c62ca"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( sqlmap )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/af5d2ea4-caf2-3067-87f7-8ed8c224ce61"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"w3mir\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5f47fe8f-f0d5-39e4-a3da-3d42d49a5ccb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = application / script (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/86f2d2ba-7ff1-3d5b-811e-a65c9d5e71be"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmouse... (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/72d7f1a8-0de8-3850-a0cb-98bd45bb0987"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onseeked (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b6da2f62-1696-300c-aee0-c14d68a3cafc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "valueOf (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/895b2f10-f744-375f-a7ed-dd2eac1b5a65"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "{:document} (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0c7fdd56-6804-3029-b647-0047a3ef77ab"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( PHP-Terminal ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2b8936c0-d823-3701-ba07-cd61908203c2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"attribute\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c99650cc-7aeb-3e3f-a853-02bd92f179ef"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = text / script (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fdf6d3c9-903b-35c9-ace1-505f4fc5a7b4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Pylot )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d992d015-1179-30a1-bbc3-178a21c4dc4b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (16)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bef1259a-3d9c-3f40-a661-8008d6a07d6e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /iys. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d720dd7b-b8de-330d-93af-65fbe7767174"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "= window; (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6ed5d5c4-f6ff-3bdd-a751-355939dbd304"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop database (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/31885b03-e1d1-3560-87d3-eaf32aad23f1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Informix error"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9aaa38d3-d22b-3b0e-a508-f7082bf6757e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onloadeddata (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a39b119c-5b5d-39db-ac97-46afd716364e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "MsgBox() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/72855bc0-220b-3908-b389-4ac98ca10c17"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"Frontbase SQL invalidation\" Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3d67b38a-ad4c-3ebe-8580-2487eb31c69c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"disco\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4249f242-9882-3dab-87a4-6328d5e1e125"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onCellChange() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/82aa7586-e5e0-3adf-a576-add591211977"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /rst.php ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/535e606e-b3d0-3da8-93e7-95b275294438"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) SQUID statistics program - calamaris"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9c84a66d-3921-3d0e-b3a4-c72fe7024bfd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Remote File/Path Include Attempt 2 (path param, ftp/ftps)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/378f8b7c-5ae1-3977-8856-2329b0cfd595"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "iframe tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f848ff86-cf3d-380d-8dc5-0afaf1067520"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_regdeletekey"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9073d984-b11e-3b38-a78b-7e44dae4757b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onRow...() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/18ed2cdd-88cf-37bc-8932-1e1969240d94"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"Microsoft Office Existence Discovery\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/28f77a9a-84f0-3316-80e3-447b85e5cd2e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onTrackChange() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a7309c46-4208-3856-ab69-7ed0bd937f37"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /rwwwshell.pl )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/64ad7a6d-9cbb-3dec-9293-259b6be94771"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /zehir.php ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bc4d5c75-4766-391e-a981-6919cce5204f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href shell (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/98a2fdbf-310d-3603-8214-89984a86bb5a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SA_FORWARD_TO\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/87460b13-bbb0-3efc-a237-18fa3eb5807e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onformchange (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/20642f5a-92f1-3b23-a3e9-2a6dc59faa50"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ inet_server_addr (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9482a45d-dbbe-34ad-a0f1-74d16f26a25d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ object_type"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/06784586-4208-30dd-b7e8-ebcda543f48c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onURLFlip() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b1f6bcd3-64fd-3c4d-8149-a0da89e3f4df"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onemptied (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bde359cc-59fc-32e4-8826-fef884114063"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ SQLIVULN_CUR_USR (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/40205483-ee64-3f3d-bda4-bf14f037e564"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "confirm (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/766b9469-1f48-3cdf-a4eb-d1ffba7f491b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"' having 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f4f1166c-c726-3c46-923d-d39d9c93581c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "touchmove (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/84a1dc92-04cc-3a1e-bee6-8c07127d20cb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Statistics Software Information Leakage (6)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c8d459e9-1399-36b3-9b65-f713f5c399f1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ondrag... (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/27baef4f-9820-3313-9b0f-506406fe386c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysdba"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c440cbbe-0403-3ff8-98fe-4362ad74f745"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"change_on_install\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/62a3b28d-a625-3b48-9174-63acec1f8e37"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ Stored procedure \"exec fn_\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c750a918-253f-345a-9ee4-3f80d2552d82"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \"/././\"(parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9d0dbaee-f0db-3746-a64b-1ba39e422b40"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /jpeg.ph )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7c6414bf-bafb-3ce7-bc07-ce255fd976ad"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like (1) \"' && 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6be796f-4a4a-3e1d-b9d5-4f1114ac0e6c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"NEWT ActiveX\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aa170840-512b-3e97-8641-65ce62747cd5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sp_oacreate"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d57e4e21-9671-36c4-8bec-686b60aec22a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Titan FTP password disclosure"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dabe4f62-f010-36f4-8ed4-05862187e362"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onloadstart (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a36fc103-6bbb-3529-9bc1-8c83b25573cf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \".../\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/27bf9437-fde0-347c-b8b0-f50ee363b0a2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Bypassing authentication in Tektronix PhaserLink webserver"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/16c1f761-8c11-378f-b545-11d3d9c16710"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Hydra )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9f9a688e-fc55-37c3-8b34-19e78db6f80c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onsubmit (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9003f087-94ce-3695-9386-ed6a4ce3c240"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ XMLFileFromClob"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1f6a3d27-41a4-3855-8c20-1976f5c9857f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ dbms_java"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c6bb2dc9-b99c-3139-8b98-ec7a1c674a00"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQLNCLI Connection String"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/310d4083-5f3c-34c3-96bf-d8ced159e0d1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ declare @"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e7ed2a91-f8be-3453-a0ec-226807a19087"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"*_id()\" sql functions (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d9189e0a-673f-3ba0-99b1-60011b99626b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onbeforeupdate (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4b6bb8c5-a12a-3c54-a68a-f190ae2718c0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onresize (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/41073193-3c48-3f78-b382-75475145b22d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onundo (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0bb44a70-6cfd-308b-8548-711d61e3067d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' OR 1 IN ( \" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5ae9f3d7-2438-3cd8-988d-5363e6d61263"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript buffer overflow attempt 4 (Response)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8186083c-1109-3bad-8573-b76069999dd0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \" or 1=1 (6) (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/28508a8f-661c-3583-9395-8275d665c842"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"big brother\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1d830ec1-3f11-3a73-9bf4-9cacc772f769"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select substring  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/175aaa06-54d6-35db-a2fa-f7d543d48d0e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ systables (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/375d1498-6133-36c7-97d0-0390070f422e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ bitand()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c9133a98-63f9-3698-a69a-8fe62ef4067e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onBounce() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fe49a802-24dc-37fb-8d2c-ed4a53c4e5c0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ into dumpfile"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ac0adbce-dcd0-3f35-b8ac-34752a73e547"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ load data infile"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5fb85f0f-5490-3b34-871d-c3cdfd070d4d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"change_on_install\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b09e2457-ba0f-3196-8641-7a702d5bf2ad"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTTP Headers Injection (Cookie)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/31fd96ca-d189-31ae-b305-0e36751b447f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ locate()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/898a28e4-bb99-3281-9517-e246fde8bc3a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (27)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/62477d83-7604-326a-9538-62461e96d31f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onkeydown (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5762d539-ff52-330c-8a53-49d9aa505f91"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmove... (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f1d6667a-1123-3a9e-b12e-8d942321a3fc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create trigger (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8d5c35ad-3526-3fd1-90ac-021055e97708"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Javascript Entity (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/87faeadd-430a-3485-ba00-4dc426483869"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) WebTrends statistics report"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b0c8c3df-4dc4-35be-9cf1-68898b7e1e06"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "BeEF HTML detection (1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b126e574-2067-36d9-b2ea-f6c62edd9232"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onabort (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/86cf76d4-716d-3c63-8b65-c436f61934c8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ REPLACE INTO (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9019c8d5-7302-3639-88ef-83d01ce38d58"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "escape() (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a86c9562-cf9c-3efd-b4f0-545075079a83"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onunload (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6bc5b5cd-263d-3dc9-bdbb-42fa9d5cfe52"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onPropertyChange() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ecdb02c2-7c4d-34e9-871c-cba43f0afe36"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XMLHttpRequest() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/41638373-8147-3374-8d40-cd9513175f79"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create table (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c232c731-fadb-346a-b05b-3aeb7f7b4c2a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"*_user()\" sql functions"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e0ae2c73-157b-3bcd-9548-1de14962c5d5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onformchange (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/09e1d261-692c-3ce2-80aa-828c0e01caae"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe (masscan)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/02ec1fc1-3dc2-3c1f-92a6-8efe737c1056"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"email extractor\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7d351d2f-59e2-3a08-883e-e8f04d93ff34"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onratechange (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/985c888f-389e-3d2f-8660-ad9476911e37"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onblur (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/026f57fe-395a-3650-8755-3187cfa3fe23"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /phpterm )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f7a5620b-f773-3ffb-b624-1b49fb506a27"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"Error processing SSI file\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/eca7f2a6-fd44-32e5-a851-07cdd0af6b49"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) ipsec.conf access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/50fe74dd-f866-3beb-8d29-df4289ebc700"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ alter table (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/90a0fbbe-a99c-3a7f-b2d3-23343ba80d00"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ syscat.dbauth (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3761785b-b73d-3357-bcc4-368b135882e9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"UPDATE SET\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/770e7359-5e7a-3e91-9ac4-998f53bf099a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src ecmascript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/852245a8-dbc8-31e5-834b-508c70d6756e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "FSCommand() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5489a540-beca-371d-ba0b-774b3f8e9894"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript obfuscation (JSF) (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fbe23d76-3566-3c5f-b8e5-fb42ace560f7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"' --\" (SQL comment) (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8b2b6781-7f89-39a5-a0c7-b669e0cdba71"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onundo (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6d2ec0e7-0414-3e33-8d8f-5c6ca5ae0a04"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( Aventis KlasVayv ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/83523918-2816-3e3e-8afa-dacc7b41e2c0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Application dir access (/manage/)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5fa7bde1-9d6f-35ef-9d70-747efb64b355"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url shell (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a53670d1-d9e8-3648-ba01-5168838699d7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"style :expression (\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/da05125b-fa1e-3a48-9c89-e43177a03525"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "escape() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5a9b525e-0535-3c08-bc3b-853ae9ef90d9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onloadeddata (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bd85e759-bda2-391f-b4bd-1e60cbf8716d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (PHP/)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9bfac234-5727-3ac2-bf79-d5ce54eb260e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (compatible ;)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e37255d0-9d79-3580-875f-fb6e4a7e9f7a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onControlSelect() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/66113cbe-28e6-304f-b1c4-5241370d5726"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CreateObject (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8d465459-dfe7-3f44-a179-310644dd2ec9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"bulk insert\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/66e00462-e41e-343b-90a7-c2498b7334e8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onunload (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/446bb1f0-d946-390b-9707-a8c745bef298"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Compaq device web interface"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d2d6b4df-2669-3fa3-9066-53841f401ecd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"curl\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6d2bb19-5287-3a89-9d7a-4f6b908e1618"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (21)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/83de9ddc-8ebb-3f1e-859e-b254d92df549"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT FROM\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2572531a-1bbf-3eba-84b5-8729ece8f6d4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"hhjhj@yahoo\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6e5aa4df-7435-3d80-a1d6-eb1ce25bb550"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CSSHttpRequest (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1995dc4b-46c7-3019-8d4f-a79c366c12c9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src ecmascript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d5dcad80-4954-3ce0-971a-c0afa24a2163"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onStart() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ad02b614-1f0f-32fc-932e-511f30862b0f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ user_constraints"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5993bc72-afce-3528-9fa7-424efab1d2f0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onactivate (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8d836e1e-702c-374f-891f-24f02ba01009"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Encoded script injection attempt ( Script.Encode )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/eca37a92-a774-3979-a359-c549d500f989"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (19)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/91cc3988-78bf-3855-b63d-8ceb8dd9febf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ null,null,null (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3324d8d5-2c0b-33e1-9e85-1828df664fcb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = application / script (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/916c5e62-8005-32e7-bf38-2c2ec50b2d33"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"/xsl/demo/adhocsql/query.xsql\" access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d72c6aaa-b091-3656-989e-e06d69a1b52a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onRow...() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/329106c2-be79-3c00-a8a2-a1e3d16020f2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Havij )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5d5d08ae-b6f1-3ca7-bb39-675b2eaea5e1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( CEHENNEMDEN ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/56b66be8-9080-3b78-898d-62af8d3d79df"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onTrackChange() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5b029991-37f8-34c6-b348-5ecd6153103b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select to_number  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/349a8858-0689-359b-b628-a8acd7dac08e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onblur (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d39b78ef-90b6-3be3-9ce1-e36abb85d541"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( zehir ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a5756046-c586-3d09-8a73-8bbaa098b3bf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe (/nonExistent)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2a23b177-6937-3d7c-87c2-18c75f55a02e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"or 1=1\" (1) (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4fc2a0be-4014-32d4-a718-d57260b35f31"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "link rel stylesheet href (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2eba69b5-3830-3f25-8b87-20129aab30ce"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ OPENDATASOURCE"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/51dcee38-e1a0-33dc-9423-b3da45e522cd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( PHP Shell ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6a81cb30-ac6b-3712-adfd-862384378c14"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onCellChange() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/72a834dd-fd0e-30a3-a595-e787add6d000"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "MsgBox() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cd35152f-7e85-3b17-a9d2-5b99b372f409"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "unescape() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aa6ca9eb-fc0c-3aea-b5ab-7ae791aec9d0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<EMBED code (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/49389822-2b2b-3511-8d4a-d4fbb958294e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ DBMS_AQADM_SYS"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/98342519-756c-341c-8675-25a232bb96bc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Nmap web server probe (nice ports Trinity)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c799e4fa-eb1c-3f75-bd5b-2f168ab9d15a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "asfunction: (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e5294d34-5921-3fc5-8c77-4c25ac7d68f7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "prompt (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c69ec67e-8691-3539-b411-dcf82987c6c4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "valueOf (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3cf7047f-2ff3-331a-b4f1-cc9841371958"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".addimport (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b622c263-0472-3d97-8e35-f9b81f8f157b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ alter column (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e0bb3cdc-f3ab-35b1-afd9-76a0e4e548eb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( Haxplorer &PHPKonsole ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/634ef1cb-5c18-3a97-af01-e8a8fd09a9b3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Analyzer for advanced web statistics page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/de38d627-5e31-3895-92e3-e72955a14779"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"digout4uagent\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0d8018f7-055b-3b72-96eb-97c3e3bb3c64"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"open()\" execution attempt"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c1db4c38-21ee-3e71-8e62-47a470d940d1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "param tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/de0f7b24-62d0-305d-a6f3-a592b716a9e3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Couldn't prepare SQL statement\" Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5a566a73-3584-3999-b0de-ebba47bcf37a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ontimeupdate (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7e9d5a9a-02e4-3a56-952e-691ad311fbac"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \".|./\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/970894bc-296b-3838-b0e6-7b3d95486325"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.cookie (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aa7e8bcb-4f98-39bb-95f3-62a2c93d538c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /jpg.ph )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d780a8b2-00d6-3968-ba3b-d82ad791cf14"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onOutOfSync() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6e824b75-a940-34cc-a5ca-08e38d54838e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"position()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/db199b26-40b3-378a-b72d-2940145c24b4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ insert into (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ff97a617-b094-3825-a39b-e118abee4fa9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Shell access ( Bad command or filename )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/04e135d0-096e-3884-a057-9d0e3c246b1f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"wget\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/73e6bd47-6c3d-371f-90f2-58d91d8b67fd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "copyparentfolder (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d6cd0a19-0c40-3fd3-808c-31c44158b560"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) HttpFileServer Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e7f75da0-2e2f-39d4-b23a-85e5e6c548f1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "touchstart (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d31c7ade-ed54-3b1f-889a-49f34a735e99"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Wordpress Hash Grabber )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9e948d10-c5ce-3eaa-b6ae-939fe7d65edc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"' and 1 --\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0a663c6b-74b9-398c-8f4d-e32da9bdaf90"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "background: url() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/295c798d-23c2-39df-833d-b4ab035bc5c1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "alert (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/984d3e72-79b1-31d2-9d73-88f3e90210a7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"and 1=1\" (6) (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5a42b9cb-ce04-393d-bb4a-e075b81c3e4f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ v$datafile (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a2f7a731-ba5a-3ea0-9d23-22980d2e7722"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onCellChange() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d2950a3c-cd40-38ea-8bec-39d24a2b6f3e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) PLESK default page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/de0785ec-8a95-3e5a-836b-9cc2a220c81c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = application / script (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3a556fd9-e6ac-3a5c-96fa-ca3e7f56fda7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( dsoul/tool )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4f972b75-2fa3-37f9-939e-3944c22e3da5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ db.members (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/76b40d94-23e3-3085-a5f7-eaf58963d041"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: expression (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/016b930b-6320-386c-accd-8dc8fd4648a3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Statistics Software Information Leakage (4)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ccc51e76-b20e-3755-96e2-dd4801379275"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \"..\\\"(Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c75ef1bd-4bf6-32a5-9a1e-b4f14c34c269"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".responseBody (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cf54e79a-7f87-30c2-b2ea-6fda539fa5d8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /lukka )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3f1413bd-b289-3b69-9106-78b2dcb3d6f7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Session Fixation Attempt - 3 (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/df2eccff-13b8-36d4-91fc-ee86d30c653c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"style :expression (\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9e325a88-8f0f-3218-afe7-592369a264f8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onafterscriptexecute (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a8dc269b-cf92-3f51-acd1-f9c7ea311da2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<OBJECT data (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cc285711-0d70-3dd7-a96f-9ea30af5a5f0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "prompt (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6e8d96a9-7d5d-3009-a6e2-ebcf52ef1252"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".documentElement (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9336b544-5111-3d64-a9a5-c74ca5bfd01d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "/backup access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6c969b2e-700a-3f78-8fee-52bd7d0c13c4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"sleep()\" (1) (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3c6dbdf9-43d2-377e-855d-8a90c8c0f9a8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onload (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c5e82311-a466-38cd-8eab-a4b36a163a48"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "background: url() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e290ec19-d742-3e4d-a502-84915b473fe7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "xmlns:ev (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2c31d8f7-154d-3645-a793-355122cc94eb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ waitfor time (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7b84bb47-46aa-3fb4-8aa2-1f24ab74e79b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onDeactivate() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fe55359d-f469-3aa2-b2f7-c662b91e1d1c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"ifnull\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/65649787-a1d7-3a6f-8621-7ca7422b19bb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "object tag: codebase (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/62ff7cb9-d75f-330c-8057-bfde33f6c82e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( c99shell ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fe091666-ddd8-3913-bce0-bf0743d3ae2c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"end-quote UNION\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a0c536c1-99f8-3e77-a96d-a13bd5d9079e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"sleep()\" (2) (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8aa3b805-6096-3123-a26d-e36f3a90ec66"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 2 (parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3fed8b70-ca52-38d2-a754-bb68001d2ab1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ alter column"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2ec48819-154e-3303-a513-6bffeebe7e74"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"8484 Boston Project\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/970b6841-3e24-3a26-be23-8edeef407acf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "seekSegmentTime() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7dbb247f-30d0-3d8b-9233-f7dcb9c07f9f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"sleep()\" (2) (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/026d902b-2f54-315c-8d9f-ec4e6caabe94"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onAfter...() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8b88c442-e0e3-3f4e-b4f4-7306e8d01fd6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Comments (1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/209436a5-4e8c-339a-b0ab-7b6696d85f02"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( cgichk )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dc0f1c63-a87f-3972-a30b-dec470e608c9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ syslogin"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a9073107-8c30-3239-bac2-89c38d6150a9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oninvalid (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4fc71f77-0a35-3482-816c-3d73d4efcfeb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT when then\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/945aa7c5-b23f-3f09-8607-5d871a0473df"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onplay (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c848ee0a-3a30-3336-8567-09674bad9a58"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "seekSegmentTime() (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a42290ba-48f0-3625-af66-2b625136438e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Escaping server-side escapes - single-quote (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e99dfe3e-3758-356d-8e05-4ccf74fe7b0d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onRepeat() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/07795e0b-d025-3008-bb69-4a5c1b49d3c2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".innerhtml (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/285c6b12-1ca4-339c-9fae-9ed6309f54b6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTTP Headers Injection (5)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7406e6c7-5b58-3e37-b8b5-243cee3dd218"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onReset() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d3070c3f-1c6d-3f16-b828-4771dca81d78"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HNAP1 access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d6282dac-350e-309e-8c5f-c7261da27163"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ information_schema (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/59c661c2-4481-3009-afe7-283629127527"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ inet_server_addr (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b8d6093b-adbe-3124-bfed-6f4022ec0d93"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ object_id"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2af17393-69e6-3923-a01c-e488e35fdf0d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /cse. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c3ba0887-c48f-39e6-9497-284c6de52929"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onactivate (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/51fc3429-8a61-3335-8785-dc446445894a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.cookie (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9b10504b-e754-3d4f-9466-b474a691cd86"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /r.php ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/71c1d8ac-d527-3e5b-8308-f78da4fda509"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like (Headers) \"or 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c3d62dd4-1381-3cd9-ae13-2a28e0f769f6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"hl_ftien_spider\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/014e818a-7f2d-3b8f-8a28-94d94bafd171"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Banner Rotating 01 exposed password file"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/baeb5687-ef5c-34e8-a4dc-4dec2ae2ac1e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 2 (headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9164df2e-4c9d-31e2-aa28-f1b08fefa953"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( NOSEC.Jsky )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d619ce83-2193-3472-af05-4bf703a2ae84"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ondurationchange (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/07445321-6422-3288-9f4c-7a9a6f67c6ed"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ ATTACH DATABASE (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6bddea16-0198-373d-86d1-d42ecd7ff71b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ REPLACE VALUES (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ac2e3e8d-950d-3089-8a37-3060a393e7a7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( ./xkernel )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f20fdde0-c993-3ab6-8083-9cf42e985234"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like (1) \"' || 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b5cd982d-6820-3449-bc57-00dae0cb49a7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ insert into (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9fa2ba3f-7130-395f-94c1-6576821d4d4a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "bgsound tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f22e5c06-34fc-3ead-8b06-e9d942721f27"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onPaste() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8b12cceb-21f4-3255-9d47-f1eca1311ca3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"nullif()\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c6738e18-19d8-3cd8-bf78-cad0984dbafe"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onshow (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8b335be8-fbe4-306e-9531-dc97caa1bb5f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href vbscript (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/10e58199-1d69-3abc-ba14-e32431b67a62"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "url shell (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a80f0de4-dd77-303d-b62d-0a618262eb29"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ benchmark() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a5542189-5be8-383a-84e6-5390e2bce42e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".documentElement (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/712e8c27-4798-3e9f-8424-90e7a797749b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onformchange (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/162e4e95-c7b8-3bdb-975e-cb2452ef5b2d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe jexboss"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bb307af1-ae9a-39b1-bc82-d85104dd3dac"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /aflast.txt )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6f268484-d9bb-3aed-8dfd-67a8ab28c331"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onLoseCapture() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c4ba3db1-8e1d-354b-926a-ab1017d3d2e3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CreateObject (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9cde5caa-f933-34b4-8efe-8988f166947a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onSeek() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9e91ebaa-6a9b-385f-9038-a3f80028c7f0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( RHTOOLS ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ffb360c3-4c56-30ce-8371-fb53aea8195d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (Zend_Http_Client)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a782f53f-f6a6-3c63-b8f2-74040375ce12"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ bitval()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1946c058-cd2c-3f15-90c1-7cc9c417c7d4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (28)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fcb80374-893e-3d58-9fa6-8540fd0a7505"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmousewheel (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b81f6ad4-83fe-3aa0-8aff-9835d5a313e2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"name()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/59d3d731-427e-3b7f-9295-6afc7b9d2a94"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "video poster (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e1acf5ea-3a54-34e6-868d-aa5e5beec64d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onHelp() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e02e24c2-fc86-3074-9433-4aa8f0ca014b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ load data infile (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/653e27cd-1c1e-3304-a8b3-18538586f867"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ syscolumns"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e7103d48-c1d0-33cc-a9f8-412ca113efe5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "livescript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a9f00fa6-b8d2-3a75-a4e1-25a65fcc74bf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Multiple applications detected in Content-Type declaration (Multipart)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/19f033c2-8967-390b-a319-2796402e9124"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cec3a168-c7ed-380b-a620-066ccd3ae005"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Bruteforce )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f9776e69-51bd-3145-812b-90f85c402446"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onundo (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f5316fc2-ec41-3d93-a63c-c25355ce4883"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( internet explorer )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f2b140eb-2412-3beb-8ca0-585c29beb523"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( NeXpose )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0ef8b70f-fcf0-3885-9798-1189742d6102"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like ' and 1=1 (6) (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/53f607e9-1d45-3f7c-93ef-7234d0302cef"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"self\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dcf28fbf-f854-38dd-b2d6-8dd58e50890d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"' && 1 --\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/63f64131-02ef-3058-845e-320564e4956e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /phpbb2_patch )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1df16d60-a5f4-33e7-a782-6166102c7a9f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Statistics Software Information Leakage (1)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/979c9ca3-3845-3c22-82d5-864489dc5c30"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"sleep()\" (1) (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bc9aaa54-7fee-3f60-b8df-8c5007dbd06f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CURSOR:url (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d8c730f3-b154-355e-bebd-aa8a13f42185"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Mosiac 1. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ec51e82c-2617-31dd-aa03-673dae2f4aa0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onData...() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c340e8ac-2a71-37ee-833e-1fdba845d19b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"preceding-sibling\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/38195722-8d5e-3647-9e4a-28e09b63f6d6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = application / x-shockwave-flash (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bc9e3153-385f-3c43-83c7-bbb874d3142d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create table (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/175b41d5-dd3c-3ca6-acd7-d3d784f4bc70"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ ATTACH DATABASE (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2678907c-c57a-3093-9da7-3fd902094854"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "getspecialfolder (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/06785f09-8bd6-3e1e-a952-db75e4f4e362"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onDblClick() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/182038bc-1dde-3fad-84c6-388455ddd47a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( w0000t )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/65f58cab-5939-3f23-9c16-377ebdc85244"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onLayoutComplete() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0e340393-6ea0-3e9a-9394-34c6743a6f1b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Max Patrol )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a3d8631a-cf0c-3ccc-ba5a-89ce1314fcd7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "confirm (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/db0f3343-208d-3eba-a5d5-8af10076d542"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( MyShell ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bff3fa10-05be-3f70-a786-b74f6dfb664f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ GRANT TO"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3d22e1f5-44c1-33b4-a0a6-3b744a30fe7e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /phpbb_patch )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7fe99c90-db6a-305b-96c0-04e78c458ab0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oninput (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fcc088f8-5a27-3992-ae1c-e86b0dbdaf82"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ join statement (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4f5c05cc-459f-3e87-9765-1a61a463f280"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ user_constraints (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/681a2825-b97c-3886-bced-fc0e81b65b5d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \"/..%c1%9c\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/96d0fd3b-a13a-388d-828a-813374c2b677"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src &# (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f1fd98f7-54f0-32bf-9d65-1fda6ad39f30"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sql_variant"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/432ef353-6ab6-3523-9b76-6b59edd5480c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Form injection (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/415b3461-6bd9-3cf5-8caf-a1cc96b76676"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Headers) (4)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/05507c87-ef78-3441-9f8f-c7ae09ce6e1c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysoledbusers (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/742ef7d2-61ae-36d1-bfa8-00577c37fa3b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysxlogins (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3ccdc790-0b6b-3ed0-856b-d18645a072f5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"*_name()\" sql functions"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a71e906c-68f5-3063-9e56-399888020d3c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"UPDATE SET\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e67a2c12-9057-3d6e-b34e-51f9bd4e6b3d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"extractorpro\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f18a477e-3773-3d72-87db-4ddad0c495ed"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Encoded script injection attempt ( Script.Encode ) (Parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/939e80cf-6af6-3196-9d39-df7aecf8ee28"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ REPLACE VALUES (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e9d14042-f853-3741-bb09-870e59f74e36"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.createElement (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fa0aa983-eb8d-3e46-8848-781329ff17b7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"Digimarc WebReader\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b9fbdad3-ee3b-3c38-8cac-e516d0da3c07"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \" or 1=1 (6) (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/66ff3b27-57e8-328f-844e-315650be59ea"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "history.replaceState() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/faeaeeac-76f5-39cc-86dd-784d12143a5f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onError...() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7289f3da-fa76-3d8e-a80c-902f460b0631"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.form (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e1599edd-1819-3bc0-9645-208a0aeec337"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onsuspend (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8ef770ba-3add-34d9-915d-81dd5c9d56ff"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Session Fixation Attempt - 4 (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/73597b6b-326a-3e9a-9bf9-4e24776ba7a7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( czxt2s )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/09dc8392-35be-3c2f-a66a-5b320d23312d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onmessage (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/28e16dbe-d8e9-3591-85e5-9a35b571d295"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"end-quote delete\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/02673dd6-a50b-3183-b77c-080b71c51274"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ msysaces (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c35c73b9-8d81-3208-85ad-af38c416ebb1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "LDAP injection attempt ( uid )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1cd760cb-da59-3031-925c-8f5901da662f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"last()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5f5729d9-98d3-3388-9d0c-3f50fa2dd478"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( pmafind )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/45cd0951-f428-3cf9-9d74-2e0e8947ecc0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create database (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/94dd5919-fc84-3bb1-89d6-e8be9131f5d0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onfocus... (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e441e205-2fc0-38cf-8daf-711028d00062"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ insert into (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/afc0c283-d666-36ad-a10c-173cc76ab5d8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (PECL::HTTP)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ecaee610-284c-38ef-bef9-61c5186ca730"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT LOAD_FILE()\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2629fa06-b873-392f-a147-4c5672aed07a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ autonomous_transaction (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2effbf31-9b21-3c16-98a1-2abd03548c92"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ UTL_INADDR (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/080f0737-eb81-30ed-ab13-cb9922bc8a40"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( Captain Crunch ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a57281aa-eb11-3936-aecc-3f13ac905eaf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ OPENDATASOURCE (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/de0956b7-e1da-3b39-a721-284038dbaff0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"or 1=1\" (6) (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/13798c62-5bfc-3c98-a7ca-fad596b0f37e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ user_users"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a50ff38c-a10d-35ab-9f5b-a8d7db71fc7a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onstalled (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bf5c83b5-b79c-32e0-9c07-273435ecab6b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /phpshell.ph )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8082ead5-cad9-306b-942e-35aacc0e3016"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"or 1=1\" (3)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aa7dab3d-bcbd-3c35-af3b-9449a7c1e703"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create function (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c6f90c56-f3d0-3484-b530-dbcbef2d8a71"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "JavaScript buffer overflow attempt 3"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5404b6da-9552-3a3a-9606-6d57be15d3ce"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT FROM\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/91c8588a-4155-365e-ba1c-4698cbbf7c96"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".open (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/024d3bda-70dd-3fa1-ae64-44e272daed58"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "alert (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/eb6e2427-e648-32c7-84ec-ce3bd5994acb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: behavior (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2114ac3a-6e87-3e1f-9be4-b749294d46ce"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<OBJECT data (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/769c36c7-3f58-3e76-99de-4895434d1e7f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "getspecialfolder (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7bfd1c50-45fc-31ce-9ce0-18f7d8482666"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "LDAP injection attempt (UID in Distinguished Name)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4fc7edfd-6f3c-35e9-b3e0-35f1b1498889"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onhashchange (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/37df9d12-3798-3c27-ad8a-ff93725d285a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DBNETLIB ASP.NET Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7db85d9f-9e2e-3ab2-a0cf-b12eaf43a01a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"zeus\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a034483b-b9c4-375a-a1cc-25f305b705cb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "input type=image (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2c0cd9a1-1107-3431-808b-fe3ebfa2ce76"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "xml tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6d07d923-6679-3030-aba3-ee60b67e92eb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ join statement (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4308aff4-bd82-37a6-a5b9-eb5ffe1cf3eb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "launchURL (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5ae40f20-443a-3ab9-bdff-ae7060474704"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "type = application / x-shockwave-flash (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d9d32ab0-f5b0-3bb1-a67b-1066190dc1db"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /proxysx. )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/27203a6a-1ef4-3471-84dc-742dee3900dd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "<BASE HREF (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/48f7439a-044a-3911-8bef-3647a3258daa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: behavior (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fcafeab7-5b9b-3654-b464-6e39b5b9cbf2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"sys.user_catalog\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5232d08a-045c-3d33-8c3b-b05e68d219a7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"mid()\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8138e35e-42cb-3c3f-b6a2-f7c59fbaa537"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Franklin Locator)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/73a3c349-b3b8-3933-845c-e9c0130c6ab1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"' having 1 --\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e20a54c2-9730-3d5f-b653-515092abd72f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onchange (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ff55022d-3c71-3e81-8675-1524eeee4091"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like (1) \"' or 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7a24bed5-4fea-3436-862d-b24dcda244d3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CreateObject (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c7e6cec4-e3fa-3933-bbc2-e2a53a9075f8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create trigger"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fd99b611-3a78-3adf-b64e-1c3861e95087"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onData...() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fedd9866-bd8d-3cda-93d0-151bfcc028c2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onhashchange (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d066ed93-103b-3242-ab09-088cef44770b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Universal PDF XSS attack (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/879b8799-4908-3944-8ee7-30458597c9b8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href vbscript (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/07d69e2e-d647-3c7d-b066-fd4433d70115"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"bew\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0effca6b-747b-3945-8f51-6e8d4f96e3b6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "FRAMESET tag (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5184886b-69e1-30aa-943e-fdac23df6d79"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "\"Microsoft OLE DB Provider\" Error Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/08ed407d-7281-3267-bc03-d1aebae19448"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ table_name"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7bd7d524-e768-333c-8163-6805ae4e1aff"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop database (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7d9e32f0-172b-37c8-982d-e09cd5a74a68"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onsubmit (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/889b8053-178f-31ab-8fe5-1804bc0b6485"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /mampus )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2b49d075-b793-3f2e-8d49-a60c0f820a5a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( jsp File browser ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1745ad4f-a239-3253-b65f-6629cd892a67"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ondurationchange (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7d059c65-ab62-30ba-9f2c-8564a835b3fe"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "pajax_call_dispatcher.php command execution attempt"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7dd70058-607c-3ab1-ab83-f541deb31cda"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".SaveToFile (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1be904e9-172f-39bf-bf8a-baa3524c6b11"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT COUNT\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b3bce80d-48b3-370e-829b-19bc002fd1db"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ db.members (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/81a7830b-2d1f-3b00-8c75-c6fa71d3f1c5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"sys.user.triggers\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/71d0c9f4-e4dd-30a8-ba00-1719de5f7651"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script target (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/80ce7a8a-3d1b-3deb-bc46-5f580c82dd7f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( newfile )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/73ad86b9-bd08-312d-8893-73289051728a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select instr (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2790b3c7-dae8-3058-aa73-0ff4d78669ff"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ constraint_type"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8855efea-8cbc-3621-9739-98eb4e0ce052"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ waitfor time (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/15838dac-5400-369d-9fa4-33b013be4833"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "textarea tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4dfb1718-9206-38d9-b7ca-fab6d753e311"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"select --\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/33aac400-4075-388d-b206-6baf8779e3d8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href ecmascript (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9ce8a984-2316-3630-a02a-1f279e0eca11"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_enumdsn"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/70780353-4ea8-3569-8e21-c65e70eba433"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "getparentfolder (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/46cfa59d-3032-3a07-ae3d-0681d465f022"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"web by mail\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/768729b6-c77d-3795-8d3a-bac339679a46"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( =ftp:/ )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4181bcda-071b-3822-b3bd-b597f0ee1977"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( News Remote PHP Shell Injection ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9c49c028-7423-3cf2-8a02-2438ffa75616"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ join statement (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6779ec38-ff55-37e9-b633-503930ca42bc"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "formaction (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/87c5fce4-9483-3f62-afa4-220e08497a93"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "div tag: binding (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8f44e589-cb05-30c1-b8cb-5a3e64552203"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "LDAP injection attempt ( gidnumber )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bc727a48-4ad3-393b-adeb-1324f1c960aa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onCopy() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bcf8ed19-1553-3c1c-9d11-455dc101d199"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"' || 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2d07d078-4e5b-3c4d-9fef-ad860320219c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT TRANSLATE()\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ad0fad9d-67c5-3875-b456-4b3cecc386cf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Atomic_Email_Hunter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bc8ef7b5-20f7-3498-954c-68793cf258fd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href javascript (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ace15bdf-d60f-3143-87ef-13709d490f63"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( cz32ts )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/86acc490-7b91-3ef5-9580-f08ad8108665"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "autofocus (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bfef4126-00c1-385a-a505-51c52e165e01"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "textarea tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6df10ef2-baa3-335e-8f5e-bb064d8db611"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create database (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5c8628d9-671c-3c2f-9634-fb869ca9250f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"declare begin\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6bdeb0bf-e4d0-3aab-867a-8ae6bea33cf5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"fantomBrowser\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3bfa348f-474e-39ad-a3fe-91958260f147"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) SQLiteManager Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3f1a2cc8-ab35-339e-b92c-4248b3182893"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ dba_users (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5821885a-858a-31d2-82b9-bfce20d39711"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".responseBody (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/43eadf26-9e4f-352b-81bb-7b3c3ad7f5e5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "iframe tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9517d3e8-43ce-3a8b-a961-60af23b5672b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "bgsound tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fc0c4233-1f3b-38f2-b9cc-52c4e8dbe17b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ create schema (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c0d37d8f-e40b-3b81-972a-6d69742f3f05"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( TL32Sn )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cb056225-8be0-3cd5-a55f-3bdf62aaa4dd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "seekSegmentTime() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4cf4bcd9-574c-3284-9409-1ba5d4b64b6e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "setRequestHeader() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c46ff0af-f18a-3cd5-a5a2-e4186bada118"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ object_name"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6f08d6dc-7533-32eb-9a57-1f2caef9d394"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ Xmlclobfromfile"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a78f2d62-11e8-3400-a9d9-660fb30bab16"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"CREATE SCHEMA\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b9295ec8-5b1e-3ba8-920c-e110d5e481ba"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onControlSelect() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/99e35215-4d39-308b-8018-a0894aec5074"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /gif.ph )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c0e961e8-925f-3977-a41c-120d9af0a2c4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "href javascript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/993b77df-424f-3754-af65-7306ed69de23"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_regdeletevalue"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aa229093-1035-32fa-b42b-8bf5be6a7e85"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "External entity injection attempt"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2d203c62-d833-305f-b304-0c879f0228fb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysremotelogins (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4c918e5e-3048-3bf0-9497-dfe750687952"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop table (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f5357c51-4fc2-37e8-b681-c0e5b4ffa1c7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ substr()"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/548b1960-b14e-3b88-985a-428501b8794e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "= document; (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f1b92944-a0f8-3b1b-b0d7-27926eaeb104"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "escape() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6e3cb57-9385-39aa-ac1b-c9f5d257fbc4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /r57.php ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bd0aa2f6-1776-3f14-81d0-3de80b32c214"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onHelp() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bbdc4e19-6ff0-338a-8260-41e671551f98"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"ALTER USER SET PASSWORD\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ce29466f-1c86-3ae8-9e0d-b530e3910a25"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".fromcharcode (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b6044652-0590-3c49-85e2-256424333eb0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onStop() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1f94b853-b52f-347a-9d37-05da7993d755"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"descendant\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/267e7dd4-1be9-3ab4-8dac-b87890a6773e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTTP Headers Injection (Location)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9df7f2dd-d243-3142-9737-6e35b60e6402"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "= window; (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4a281569-0add-3b67-8f1c-9834a104ff30"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onCut() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f1d3bafb-c98e-3a8a-99e1-a6c97ca1d098"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onPause() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7ed42ef7-cb7c-3c73-8c32-01547887e760"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "getFromURL() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/15b85e6e-9371-32b2-8d43-c063923290b3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onURLFlip() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/88a99911-3edf-3cd2-b125-3c5f54a87017"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysprocesses"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8e00a9c8-ac49-3d09-91ef-ccc1e6499c3e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sqlite_version (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0459ddd6-347c-3d2f-b5d7-c2a224f7042d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"sleep()\" (1) (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/913a3d46-7371-33f2-a3fa-e8f5322884f4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /sql.txt )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/dccd2242-97dd-3498-b0a8-4c066d7594e7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( PHP Commander ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e8876976-37ed-3ab7-84e5-52901d031e06"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "= document; (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2a1ac913-8bd8-3c92-8c03-e76e7b9ff902"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Remote File/Path Include Attempt 1 (path param, http/https)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/726e93f5-2b72-35f8-80e0-3bfaf4552e1c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "[window] (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c9b54151-31ed-303b-9809-187cafdf116f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "window[] (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/297d3468-fa78-369a-9336-ace056e5e719"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Exception (0x80131904) Message"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/af2ae43c-8fc5-3f57-9781-090be3ddf02e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onemptied (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ff70e9ca-5af9-3f49-b42a-9681929cdc35"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onchange (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/03d46591-4b92-3844-85c3-5f4142e10571"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "window.document (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7a0fdcdc-0d8a-3860-a0ea-98e69470fdeb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "eval; (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4047b269-3eef-38a2-be3c-199fb6d1d9af"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ CONVERT( (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ffc9dc34-a7c1-31a8-8aaf-508d9a2d2b60"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTML comment (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e36db81f-8971-3380-9529-6957f3a3540c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onpopstate (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/456b1c4f-8178-3c21-8201-fe08acea0b36"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ mysql.db (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e762db6e-0b1b-3d2e-bd1f-a30f95e317c5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ like \" ' && 1=1 \" (Parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f69547af-93cd-3f8b-a424-6f8877fcf57c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ expressions like \"' or 1 --\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b4c08727-90eb-33f4-b136-468f15c3d733"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onCut() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ec004c4c-f16f-309a-81c1-63aa5f09f3d5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( CEHENNEMDEN ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/89526e43-ec3e-3210-b5d3-17161d27fea5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ waitfor delay (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b1988e13-fd03-3b42-9d78-d3ed86a23556"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"ALTER USER SET PASSWORD\" (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/30e8783a-1299-3f15-bc7a-0035d587d584"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "eval() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6b31f453-8ad7-36be-8034-821b5212072d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ msysqueries (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fb3ce41e-29dd-3ae0-894f-dcba1f075fe6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access (http client)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a7fb2831-1d22-3959-9d10-93f2b1feeb30"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ openrowset"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c5ce6c7b-5222-37ba-8456-3926cee60d54"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script target (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0b37acdc-1b4f-369f-a7a7-706587bfaf32"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "oncanplaythrough (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d68e5652-d6d4-3247-a87c-6ef4e527c68d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"CREATE USER SET PASSWORD\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d06b0776-9f14-31b2-ab0e-f974113dc8ef"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".ShellExecute (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/af0d05ad-fc98-3095-ac41-6880e4674d0c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "window[] (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a6f0b816-950a-3632-af60-d7caff394689"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onsuspend (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/49f66175-bffb-39ec-865e-ed815ee33db7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"FooBar/42\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/708ea164-5557-334a-bb1d-61f6ae5ba68b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onScroll() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4067f234-8bff-3319-b5d8-c5c57c47b8df"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ owa_util"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/08c1a7ec-1873-313e-9259-128ded8e6c7f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CURSOR:url (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f8b57729-e51e-3cfa-bc3a-055a80cdc36c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "DOS \"Double-precision floating-point number dos attack\" (Headers) (5)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/bc87b4db-b1ab-3a91-abb5-bd740dff0949"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (7)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b4c79a77-c100-3d7e-9599-343623f7f88c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ insert into"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/aa35ddbc-0dc7-3e7b-9226-2080a38f12c7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT IF()\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/912ada26-2f76-3c45-867a-3cf948cccbd9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"fastlwspider\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/acc1c19f-3b68-3ea9-b377-f7fbbb3e82af"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "mocha (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1f91bc8b-0de3-32b1-944f-0e77a067304a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( T H A T ' S  G O T T A  H U R T ) exploit"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/87a038ec-18ac-3916-afc8-3731357bdb16"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SUBSELECT RETURNS\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/01a9e661-4b9f-39d6-a222-84512466ecb1"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ load data infile (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/84e5fdbf-5fdb-300e-b23c-528577124e22"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src &# (Headers) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a9e94362-b89e-3de3-a551-d9f5fdc6764c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src vbscript (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/56b05520-786d-3d48-ae83-35025cd9b636"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script tag end (Parameter) (2)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4fc4645f-92eb-31b1-a3d5-cad2b660fec8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onseeked (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e83ce04b-6a64-3078-90ce-fed47d85c7e7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( /php.txt )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a700a8e5-efd3-3af3-a74f-329ff13c61ab"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Havij SQL injection (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8705feee-bd2e-346a-8023-69829c10432e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "alert() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3d323213-7861-3fdc-8f3c-a3d715c04e38"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "applet tag (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d50f15a9-c67d-3d0d-bca2-1ad6d37d0c11"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "/warez/ access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0cdc9c80-fbdb-3e29-a398-ea27cb8c3906"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"emailreaper\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/cabcc967-59fe-3f89-a1e8-3729deed4612"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Indy Library)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/ce03d58b-915d-379f-b0b7-45ce513aed51"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "touchend (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3c16150d-819b-3c58-8af7-d0966c339a99"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onkeyup (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3f15b8ed-0a84-376e-b121-7bf3fab09a5f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "prompt (URL)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a5bd6201-5b5d-3907-9d60-f5b07e28d55a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document.createElement (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a28b4981-96ae-348c-893f-1d19a8e24855"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"preg_\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c86a7cd9-f3cf-3322-806b-aab99e0b81eb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "copyparentfolder (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a99a8bf3-c933-325c-963a-c020f27418f6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 3 (parameters)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8aaf8491-75e7-3dd6-9570-d1c930efa974"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"CopyGuard\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/761c33a5-9027-32ea-ad76-1306353d676d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Generic Format String attack attempt 4 (headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1e0d3040-1cb8-37ed-a272-5382251c7cd3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"packrat\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0a07ecc4-d7de-3f35-868a-b003cf3bb0c8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"DBMS_SQL\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d08ef9fc-3cd0-3e69-9974-02f8dfbdd038"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select instr  (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7df72a18-c861-39f8-b2a7-aac0a1dba5b4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XMLData. (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/379174e9-b309-369f-9690-1baf5199ad31"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ select substring"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/eb9b4c4a-c50f-3431-8aa5-62e38f5c0fd3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ systables"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f5eb23f6-dd71-398c-b6f8-1d191b4486d9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onpopstate (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3293ef25-3e70-3b02-84ea-3fc0fe4d1282"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"ancestor-or-self\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/14358f66-2552-3dcb-9098-4147438c2fa7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (20)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/e67bf862-5245-3078-928d-4638225bf7e0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "getparentfolder (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/58853cac-7f7f-3d41-a4b2-3d2ae9be489f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ alter table"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1ea7b029-ceff-3f2c-9e48-27648c00c37c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ drop function"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/248a9454-aa3a-326f-a4f3-9cccce400b0e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ CONVERT( (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d25c69c6-c3cf-366b-bb2c-5ba187616a8e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Nessus ) - 3"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6f079f92-9701-32ee-a6c1-324879ad3f1e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ sysdba (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fcd86d89-4719-3bd3-b3ea-02e14fed2cd9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document[] (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/422dee9b-f7f2-3a8e-9f5b-fb9880e6a38b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) General error"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/814dc5f9-6a84-3cdf-83fb-d5eff6fea83e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onDrop() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5882b822-070f-3a02-8616-781a1ca888f6"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Session Fixation Attempt - 1 (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/156cd09e-1204-3597-b989-701c88292000"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ owa_util (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/99f430c6-5b55-3db1-8353-dc7f4b24185b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ GRANT TO (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/58372097-aa85-376e-b108-dfb704203cd2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"fn:id\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/56098124-4804-3721-b823-02c6bdda9794"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ DBMS_AQADM_SYS (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/502bdf35-d9f2-354c-bed4-5feef534a58c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ xp_regenumkeys"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f1344627-ca30-3109-bdc1-86122eceb123"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": ".FileSystemObject (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/51b3cf36-cc13-30ba-b588-a907958b4ddb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SELECT when then\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7a24e946-2287-3ca6-8b96-7b858b46cc58"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"end-quote delete\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5f28d1c8-2686-3717-9b96-217f26024b62"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (ContactBot)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/340eced1-76af-3254-bd18-3a659c5036cd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"Shockwave Flash\" spam bot"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/12539efa-d86e-3001-8a1d-16af89bc6588"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"end-quote select\" (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7127da55-ad9f-3227-bb85-e99e16ef4089"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"SA_EXEC_SCRIPT\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c19adeb8-b998-33d3-b570-375b305e79f3"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"Crescent Internet ToolPak\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b30ece57-fca3-380c-a28a-e1499b536a13"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Comments (3)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9540a91e-a82d-32f5-8aa1-07178af04940"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "input tag: dynsrc (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/baab57aa-fe64-3087-9e49-35c19800cf17"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"perl\" (corrected)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c45db1a4-00e1-3853-9636-e36846a95e44"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "HTTP Response Splitting (1)(Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/d5a2792e-bddd-3ba7-9f8a-2bc6875729e9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ inet_server_addr (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c166d7ad-fd5f-3cc9-ac09-ed59c73c7070"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Fastream NETFile Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/07f090e4-b709-3870-80e8-0107fc0f32fb"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ null,null,null"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5d582600-fa9b-3f5d-a005-343a0789be86"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onCopy() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b4a74bca-a628-36de-9e93-08b2c3e461cd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL Information Leakage (24)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fd6d0332-a9e0-3f61-aa74-820e41dcd851"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onTimeError() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f718aa54-0798-3dd3-b818-8f0e57fb658d"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onReverse() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8db66654-a24e-33c9-b116-2dae8a5ceaf4"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"floodgate\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/75108d02-78e0-3aa1-8618-e43c5d631b19"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( zehir 2 ) upload"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/64f75e85-3e22-39e0-8c5b-b8ed70c63e24"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "applet tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/46c31f2c-8c3a-3223-b5a5-4bb5dac787c8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onMedia...() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/37001d74-3694-346f-b49a-12fafd9872ad"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler \"shai\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/76e42af5-8290-3e42-a91e-d85777068f45"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ db.members (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f16cc9ed-db00-3d84-8a54-db52865b2885"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onclick (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/57c3e81b-6ec8-3873-bdb7-16d57052fd33"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Directory Traversal attempt \"..\\\"(parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/76e862df-c92a-30af-b1e7-c39f6e8e4e67"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "CreateTextFile() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/8ec75190-2002-3d23-9064-25fd4037c720"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style: background-image (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0ed28c7b-7d1c-3f62-a366-cedf914d0987"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( Qualys-Scan )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0153b58b-de7a-3fa9-ac33-600c3179ebfa"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "ontimeupdate (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1949b7d0-304f-3ad0-bf1b-a2a50a047c6b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (Demo Bot)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f35d6749-9ea4-3bed-a60f-f16561af3a19"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "document[] (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b63176c2-88d6-386e-8aa3-fe1048e30ef5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XSS script tag (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/c2cd6d1a-42a0-34e5-a50f-4f7e6ff94ace"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( xmlrpc exploit )"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/483196a7-9c4c-3a1b-a17b-54e7318705fd"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "urn() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/2c976aaa-f0f0-3c65-a19c-cdce61866fbf"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ integer field UNION (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4529d065-bf65-3629-ba2f-6a7dabf4f47c"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "-moz-binding (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/5828e9d2-2b7f-3cd3-a005-91eab91bce7e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "style display:none (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/545dae54-36f0-335a-8ccf-62e7b7d16398"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "XPath Injection \"following\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/fb8f2ff0-9e50-38b2-bbf6-6b180620388b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "object tag: codebase (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/3109f7da-c7ba-3f26-a9f8-ca34acaee376"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "(GHDB) Web File Browser Page"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a720beae-f66d-319e-bdde-670ef05506a9"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onforminput (Header)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/a54c8cb4-02e4-3623-bcb1-60e1a2befb72"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ tbcreator (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0931774d-2b6c-32b7-a614-afb66296421a"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ instr() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/6baeb045-8e01-3eda-a7f5-3406f62fe568"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "input tag: dynsrc (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/793b6788-5bd4-32e9-8dd2-ade5dbdbd480"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onSeek() (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/59dadd97-e5ee-3e71-a6ef-dc3410c78222"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Automated client access \"libwww\""
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/b691ed46-80e2-3788-a992-9b7c1ead102b"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onProgress() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/1b6da43f-2233-35cd-b87b-f8b01ae82870"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( zehir ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/17184650-3b8c-360b-92dc-cbae7414e456"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ GRANT TO (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/0f02d8c9-4e20-3743-8d5e-1eec8a1414a2"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onload (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/481041ab-e873-3edc-98c7-259d7c80ba31"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious Web Site crawler (ZmEu)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/4efe9aaf-1b54-377a-9415-3c9784422b85"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ \"select 0x\" (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/9977152e-d3da-3a20-91c0-2db95896f931"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onplaying (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/7fadfc19-3961-3293-9fe7-5b41384b96a7"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onabort (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/18c3320d-4114-3353-b855-639d3c9dca6f"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ current_timestamp() (URI)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/97474abb-b806-34a0-baf2-d240d2b516e8"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Malicious program ( Remote Explorer ) access"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/886f02ce-81b4-339e-bb21-924ecb17e816"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "onBefore...() (Parameter)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/53c87257-86a0-39d6-a97b-1395c3782787"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ information_schema"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/f0aee28b-c035-3f9e-b2ba-f090aa68a8f0"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "SQL-INJ pg_attribute"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/97f1a80c-3158-39c1-8e43-6f232fc92af5"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "src http: (Headers)"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/760031b9-3266-3885-84fe-e2ca55671f5e"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Invalid UTF-8 for Directory Traversal"
                    },
                    {
                        "signatureReference": {
                            "link": "https://localhost/mgmt/cm/asm/working-config/signatures/37c6330f-c9af-36c2-8177-d80337367d49"
                        },
                        "enabled": true,
                        "performStaging": true,
                        "name": "Web Server Probe ( NeuralBot )"
                    }
                ],
                "name": "signatures",
                "id": "006fcd4e-b57c-3714-aede-6bb66938a9a6",
                "generation": 1,
                "lastUpdateMicros": 1479388438674931,
                "kind": "cm:asm:working-config:policies:signatures:policysignaturearraystate",
                "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/signatures/006fcd4e-b57c-3714-aede-6bb66938a9a6"
            }
        ],
        "generation": 2,
        "lastUpdateMicros": 1479388438906235,
        "kind": "cm:asm:working-config:policies:signatures:policysignaturecollectionstate",
        "selfLink": "https://localhost/mgmt/cm/asm/working-config/policies/1005831c-7e40-30ed-bd0d-f8068526d7ef/signatures"
    }

3. Perform a POST operation with the new attributes to a special URI that updates policy signature attributes.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform a POST operation with the new attributes to a special URI that
updates policy signature attributes. The URI is the string
"/signatures/update" appended to the policy selfLink. The POST data
contains an array of updated signatures. Use the signature selfLink as
obtained in step #1 as the link attribute of the 'signatureReference'
structure. Choose the 'enabled' and 'performStaging' values as needed.
Note - the example shows one signature in the 'updatedSignatures' array,
but multiple signatures can be chosen.

::

    POST: https://<mgmtip>/mgmt/cm/asm/working-config/policies/<policy id>/signatures/update
    {  
       "updatedSignatures":[  
          {  
             "signatureReference":{  
                "link":"https://localhost/mgmt/cm/asm/working-config/signatures/152bcf94-4ab3-3f8b-b524-4648f83249e0"
             },
             "enabled":true,
             "performStaging":true
          }
       ]
    }

The following is the JSON response from the POST operation:

::

    {
        "updatedSignatures": [
            {
                "signatureReference": {
                    "link": "https://localhost/mgmt/cm/asm/working-config/signatures/152bcf94-4ab3-3f8b-b524-4648f83249e0"
                },
                "enabled": true,
                "performStaging": true
            }
        ]
    }

API reference
~~~~~~~~~~~~~

`Api reference - asm signature
management <../html-reference/asm-attack-signatures.html>`__ `Api
reference - asm policy
management <../html-reference/asm-policies.html>`__
