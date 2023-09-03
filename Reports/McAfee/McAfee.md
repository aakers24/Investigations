## McAfee Spam/Phish

Date Recieved: 9-1-23

Date Analyzed: 9-2-23

Notes:

* I recieved 2 emails from "McAfee". The first was at Fri, 1 Sep 2023 15:20:25 -0700 (PDT), and the second was at Fri, 1 Sep 2023 17:44:27 -0700 (PDT).

* This seems to be at least partially designatable as a sort of Homograph attack as the "McAfee" sender is clearly in some non-standard character set.

* The first email's sender is from the domain `anderson[.]assocmicroscope[.]com` which has an untrusted/malicious reputation according to Talos.

* The email is basically just one big link to `hxxps[://]storage[.]googleapis[.]com/fh4gh8j1x7723s0bpy/z909o3g3k1cc9nxzkj[.]html#OfOvuJg061qQFk8aL3ki[.]AwQllRgnSnTnGmdtPU?ffRL5gccT597cy7JQcdcW5cKc9jcBhF0fcbbb5c`

* From `urlscan.io` I can see that it's a link to googleapi (obviously) that initiates 3 http transactions. Primarily, it tries to download an HTML file `z909o3g3k1cc9nxzkj.html`. It also eventually tries to access an address on the domain `bedtimesnap[.]com`. Both URLs in this redirect chain have questionable reputations on Talos.

    * bedtimesnap never responded and I believe this may indicate that the attack has already been addressed or shutdown.

* The second email is nearly identical to the first except for the literal sender and a slight difference in the link contained in the email body. Despite the small differences in the googleapi link, the link still tries to access the same HTML file and tries to navigate to bedtimesnap via listkind the same way the first email did.

    * The domain that the second email was sent from is `scott[.]pearldives[.]com` which has a better reputation of neutral.

    * When the second email link tried to go to bedtimesnap, the request didn't fail.

* After some sleuthing around using website resources found on the `anderson[.]assocmicroscope[.]com` website using `urlscan.io`, I found a common resource that has been used in the previous months/years and it looks like similar websites have been coming and going for some time.

    * By taking the hash of this file from the indicators on urlscan and plugging that hash into a virustotal search, I'm concluding that it is a spy pixel or something of the sort.

* The pearldives website is just an "under construction" image.

* When I attempted to access more files by following some of the links in a sandboxed, proxied environment I was given errors that meant they either shutdown/corrupted their assets/infrastructure or had some security in place.

    * I believe the access denial was googleapi security because the way I was trying to access. I went around that and ultimately came to the conclusion that the destination file is empty. I get End of Page errors when trying to browse to it and the indicator hash from urlscan shows up as an empty file on virustotal.

* I don't know what the reason for this would be. It could be testing, it could have gotten taken down by the threat actor, it could be a mistake, or something else that I won't figure out as I am satisfied with the extent of my investigation into these emails at this time.