# Level 3: Glasshouse

## 1. Which user identity was compromised (patient zero)?
As is highlighted by the case files, **e.novak** is the compromised user. <br>
<img src="image/level3-q1.png" alt="Actor" width="250" /> <br>

## 2. What technique bypassed MFA during initial access?
The technique employed here is to capture session tokens to force the MFA to give credentials to the threat actor. <br>
<img src="image/level3-q2.png" alt="Actor" width="250" /> <br>

## 3. What provided persistence in the cloud identity plane?
In the event and audit logs we can see that they use the captured session tokens to set up **illict OAuth consent** so that they have a permanent way in. <br>
<img src="image/level3-q3.png" alt="Actor" width="250" /> <br>

## 4. Which app permission scopes were abused for mailbox access + BEC?
In thesession and token forensics we can find an alert that identifies **Mail.ReadWrite and Mail.Send** as our permission scopes. <br>
<img src="image/level3-q4.png" alt="Actor" width="250" /> <br>

## 5. What mailbox rule did the attacker use to conceal the fraud?
Back in the event and audit logs we find an alert that indicates a new mailbox rule was created. By looking at the specifications of the rule we can identify that it would be used to hide the messages for the fraud. the actual rule is **Inbox rule created (blank name). ForwardTo: external; MessagesContaining: "invoice","bank","payment"; Actions: MoveToFolder "RSS Feeds", MarkAsRead, DeleteMessage.** <br>
<img src="image/level3-q5.png" alt="Actor" width="250" /> <br>

## 6. What was the ultimate fraudulent action (impact)?
In the same place we can see that a wire transfer for a large sum of money was made after changing the information for a vendor (presumably the account details to redirect the funds) <br>
<img src="image/level3-q6.png" alt="Actor" width="250" /> <br>

## 7. Which vendor was impersonated in the payment-redirect fraud?
In the same alert as the previous question we can see that **Meridian Logistics** was the effected vendor. <br>
<img src="image/level3-q6.png" alt="Actor" width="250" /> <br>

## 8. What is the AiTM phishing / proxy domain used for initial access?
In the network captures section we can find an alert that tells us that **login.kestrelpay-sso.com** resolves to the attacker proxy. <br>
<img src="image/level3-q8.png" alt="Actor" width="250" /> <br>

## 9. From which country did the malicious sign-in originate?
A look at the threat intelligence tells us that this attack originated in **the Netherlands** <br>
<img src="image/level3-q9.png" alt="Actor" width="250" /> <br>

## 10. The DBA d/p.hollis exported a customer database. Is that part of THIS intrusion? (yes / no)
As we've already established, the goal and action of this intrusion was a fraudulent wire transfer. Moreover, this user was not compromised by this threat actor. <br>

## 11. Logs contain a user-agent implicating "CRIMSON JACKAL". Should you attribute to them? (yes / no)
No, the vast majority of evidence points to a different threat actor. If anything, this other actor is either a red herring meant to throw investigators off or the ones responsible for the afformentioned customer database exfiltration. <br>

## 12. Which threat actor is ACTUALLY responsible?
By once again looking at the threat intelligence, we can see that **FEATHERED SERPENT** is actually responsible for this breach. <br>
<img src="image/level3-q9.png" alt="Actor" width="250" /> <br>
