---
title: "Game 1 – 04"
description: "https://sourcing.games/game-1/game-1-wdd47k/"
summary: "Game 1 – 04"
date: 2024-02-09T06:37:46+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "SOCMINT", "email", "sourcing-games", "game1", "game1-04"]
canonicalURL: ""
showToc: true
TocOpen: false
TocSide: 'right'  # or 'left'
# weight: 1
# aliases: ["/first"]
hidemeta: false
comments: false
disableHLJS: true # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
# UseHugoToc: true
cover:
    image: "images/cover.webp" # image path/url
    alt: "Cover: Sourcing Games Logo" # alt text
    caption: "" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game1-04/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

I met [Willow](https://www.linkedin.com/in/willowhorton/) a few years ago, and she helped me with some things at recruitment.camp. To speed up our communication, I gave her an email at recruitment.camp.
But I had to learn how to create a professional email address, especially Willow didn’t want to have a dot in the email address.

Her email is the password to the file below (Download file).

Hint: Don’t let bounce, disposable, spam-trap and deactivated emails decrease your sending reputation.

**Note:** _Do not contact Willow or the owner (me) of recruitment.camp via email or contact form on the site!
Be a sourcer, the **hint is enough**. Spamming will get your IP blocked._

**Veuillez ne pas jouer à ces jeux, si vous ne pouvez pas suivre les règles simples ci-dessus!**

<p style="text-align: center;"> <a href="https://sourcing.games/wp-content/uploads/2022/06/willow.docx" target="_blank" rel="external noopener noreferrer" title="willow.docx"><b>Download File</b></a> </p>

<p style="text-align: center;"> <a href="files/willow.docx" title="willow.docx"><b>Mirror</b></a> </p>

## Instructions

Find the e-mail address and open the file containing the password for next level.

## Solution

The file is a `.docx` file. I opened it with LibreOffice Writer and it password protected. Based on the description, the password is Willow's email address. So, I need to find her email address.

![docx file](images/docx_password.webp#center)

We can click the [Willow](https://www.linkedin.com/in/willowhorton/) name in the description and it will open her LinkedIn profile. I found her full name is "Willow Horton".

![Willow Horton LinkedIn Profile](images/willow_horton_linkedin.webp#center)

When I click the `Contact Info` button, There is no email address.

![Willow Horton LinkedIn Contact Info](images/willow_horton_linkedin_contact_info.webp#center)

Based on the hint, Willow's email address is at `recruitment.camp` domain. Also you can confirm it by visiting the company's [Terms of Service](https://recruitment.camp/terms-of-service/) page. It's mentioned that the company's email address is `support AT recruitment DOT camp`.

![Recruitment Camp Terms of Service](images/tos.webp#center)

So, we can use search engine like Google to find her email address. I used the following search query:

```plaintext
"Willow Horton" email site:recruitment.camp
```

But it didn't return any result.

{{< figure align=center caption="Google Dorking" src="images/google_result.webp" >}}

Based on my experience, there are some common email address formats used by companies. Such as:

```plaintext
1. firstName+lastName@example.com
2. lastName+firstName@example.com
3. firstName.lastName@example.com
4. lastName.firstName@example.com
5. lastnameInitial+firstName@example.com
6. firstName+lastnameInitial@example.com
etc.
```

Example:

```plaintext
1. willowhorton@recruitment.camp
2. hortonwillow@recruitment.camp
3. willow.horton@recruitment.camp
4. horton.willow@recruitment.camp
5. hwillow@recruitment.camp
6. willowh@recruitment.camp
etc.
```

To automate the process, we can use a tool like [Email Permutator+](http://metricsparrow.com/toolkit/email-permutator/). Enter the first name and last name, and the domain name and click `Permutate` button. It will generate the email address permutations.

![Email Permutator](images/email_permutator.webp#center)

Result:

```plaintext
willow@recruitment.camp
horton@recruitment.camp
willowhorton@recruitment.camp
willow.horton@recruitment.camp
whorton@recruitment.camp
w.horton@recruitment.camp
willowh@recruitment.camp
willow.h@recruitment.camp
wh@recruitment.camp
w.h@recruitment.camp
hortonwillow@recruitment.camp
horton.willow@recruitment.camp
hortonw@recruitment.camp
horton.w@recruitment.camp
hwillow@recruitment.camp
h.willow@recruitment.camp
hw@recruitment.camp
h.w@recruitment.camp
willow-horton@recruitment.camp
w-horton@recruitment.camp
willow-h@recruitment.camp
w-h@recruitment.camp
horton-willow@recruitment.camp
horton-w@recruitment.camp
h-willow@recruitment.camp
h-w@recruitment.camp
willow_horton@recruitment.camp
w_horton@recruitment.camp
willow_h@recruitment.camp
w_h@recruitment.camp
horton_willow@recruitment.camp
horton_w@recruitment.camp
h_willow@recruitment.camp
h_w@recruitment.camp

```

<p align=center>There are 34 emails generated by the tool</p>

After that we can verify the email address using a tool like [email address verification tool](https://tools.emailhippo.com/) from [Email Hippo](https://www.emailhippo.com/). Enter the email address and click `GO` button. It will check if the email address is valid or not. But, skip the email that contains dot (`.`) in the email address. Because the description mentioned that Willow didn't want to have a dot in the email address.

> "But I had to learn how to create a professional email address, especially Willow didn’t want to have a dot in the email address."

After inputting some email addresses, I found the valid email address. Which is `hortonw@recruitment.camp`.

![Email Result](images/email_result.webp#center)

### The Hacker's Way

You can also use some brute force tools to find the password, such as [John the Ripper](https://www.openwall.com/john/), [hashcat](https://hashcat.net/hashcat/), etc. So you don't need to verify the email address one by one.

In this case, I used Hashcat to crack the password. I don't know when using John the Ripper the cracking process is failed with the error message `No password hashes loaded (see FAQ)`. The command I used is:

```bash
john --wordlist=email.txt hash.txt
```

Because of that, I used Hashcat instead.

To crack the password using Hashcat, we need to do the following steps:

1. Copy the generated email addresses to a text file. Example: `email.txt`
2. Get the hash of the `.docx` file using `office2john.py` script from John the Ripper. You can download the script from [here](https://github.com/openwall/john/blob/bleeding-jumbo/run/office2john.py). The command is:

    ```bash
    python office2john.py willow.docx > hash.txt
    ```

    *The `hash.txt` file will contain the hash of the `.docx` file.<br><br>

    ![office2john.py](images/office2john.webp#center)

    But, Hashcat can't crack the hash directly. We need to modify it a bit. To do this, all we need to do is delete the string `willow.docx:` in front of the hash so that the hash looks like this:

    ```plaintext
    $office$*2013*100000*256*16*2eeab931fa9e5ff11ccdb3f914b94097*16924192d4df74f4ef0182357c4ae292*84fa257b4baa1e107b9c0368bc0b711e6d6905048a5b4e1ec7ec1a16284176ff
    ```

3. Crack the hash using Hashcat. The command is:

    ```bash
    hashcat -a 0 -m 9600 hash.txt email.txt
    ```

    * `-a 0` is the attack mode. It's a straight mode.
    * `-m 9600` is the hash type. It's for MS Office 2013 files.

    {{< figure align=center caption="Hash Modes from `hashcat --help`" src="images/hash_modes.webp" >}}

    ![Hashcat Command](images/hashcat_command.webp#center)

4. After the process is finished, we can see the password. Which is `hortonw@recruitment.camp`.

    ![Password Cracked](images/password_cracked.webp#center)

I used the email address as the password to open the `.docx` file and we can see the actual password of the challenge:

![docx file](images/docx_correct_password.webp#center)

## Flag/Password

<details>
<summary> Show </summary>

`sourcingfun`

</details>

## References

- [John the Ripper Documentation](https://www.openwall.com/john/doc/)
- [Hashcat Documentation](https://hashcat.net/wiki/)
- [Password Cracking - Cracking MS Word .docx lab from AttackDefense Labs](https://attackdefense.com/challengedetails?cid=110)
- [How To Access Password Protected Microsoft Files](https://blog.hackerassociate.com/how-to-access-password-protected-microsoft-files/)
- [Extracting Hash from Password Protected Microsoft Office Files](https://medium.com/@klockw3rk/extracting-hash-from-password-protected-microsoft-office-files-b206438944d2)
- [12 OSINT Resources For E-mail Addresses](https://nixintel.info/osint/12-osint-resources-for-e-mail-addresses/)
- [OSINT - Simple tips #5 - Email addresses](https://cylab.be/blog/123/osint-simple-tips-5-email-addresses)
- [Discovering Hidden Email Gateways with OSINT Techniques](https://blog.ironbastion.com.au/discovering-hidden-email-servers-with-osint-part-2/)
- [It’s a Match! Combining Tools & Methods for Email Verification](https://keyfindings.blog/2018/11/16/its-a-match-combining-tools-methods-for-email-verification/)
