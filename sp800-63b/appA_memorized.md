<a name="appA"></a>

## Appendix A&mdash;Strength of Memorized Secrets

*This appendix is informative.*

Throughout this appendix, "password" is used for ease of discussion. Where used, the term should be interpreted to include passphrases and PINs as well as passwords.

### A.1 Introduction

Passwords remain a very widely used form of authentication [[Persistence]](#persistence) despite the widespread frustration with their use, from both the usability and security standpoints. Humans have a limited ability to memorize complex, arbitrary secrets, which often leads them to choose passwords that can be easily guessed. To address the resultant security concerns, online services have introduced rules intended to increase the complexity of these memorized secrets. The most notable form is composition rules, which require the user to choose passwords constructed using a mix of character types &mdash; such as at least one digit, uppercase letter, and symbol. However, analyses of breached password databases reveal that the benefit of such rules is not nearly as significant as initially thought [[Policies]](#policies), while the impact on usability and memorability is severe.

The information theory concept of entropy [[Shannon]](#shannon) is often used to characterize the complexist of user-chosen passwords. While entropy can be readily calculated for data with deterministic distribution functions, estimating the entropy for user-chosen passwords is difficult and past efforts to do so have not been particularly accurate. For this reason, a different and somewhat simpler approach &mdash; based primarily on password length &mdash; is presented herein.

Many attacks associated with password use are not affected by password complexity and length. Keystroke logging, phishing, and social engineering attacks are equally effective on lengthy, complex passwords as simple ones. These attacks are outside the scope of this Appendix.

### A.2 Length

Password length has been found to be a primary factor in characterizing password strength [[Strength]](#strength) [[Composition]](#composition). Passwords that are too short yield to brute force attacks and to dictionary attacks using words and commonly chosen passwords.

The minimum password length that should be required depends to a large extent on the threat model being addressed. Online attacks where the attacker attempts to log in by guessing the password can be mitigated by limiting the number of login attempts permitted. In order to prevent an attacker (or a persistent claimant with poor typing skills) from easily inflicting a denial-of-service attack on the subscriber by making many incorrect guesses, passwords need to be complex enough that rate limiting does not occur after a modest number of erroneous attempts, but does occur before there is a significant chance of a successful guess.

Offline attacks are sometimes possible when an attacker obtains one or more hashed passwords  through a database breach. The attacker's ability to determine one or more users' passwords depends on the way in which the password is stored. Commonly, passwords are salted with a random value and hashed, preferably using a computationally expensive algorithm. Even with such measures, attackers' current ability to compute many billions of hashes per second with no rate limiting warrants passwords intended to resist such attacks to be orders of magnitude more complex than those that are expected to resist only online attacks.

Users should be encouraged to make their passwords as lengthy as they want, within reason. Since the size of a hashed password is independent of its length, there is no reason not to permit the use of lengthy passwords (or pass phrases) if the user wishes. Extremely long passwords (perhaps megabytes in length) could conceivably require excessive processing time to hash, so it is reasonable to have some limit.

### A.3 Complexity

As noted above, composition rules are commonly used to increase the difficulty of guessing user-chosen passwords. Research has shown, however, that users respond in very predictable ways to the requirements imposed by composition rules [[Policies]](#policies). For example, a user that might have chosen "password" as their password would be relatively likely to choose "Password1" if required to include an uppercase letter and a number, or "Password1!" if a symbol is also required.

Users also express frustration when online services reject attempts to create complex passwords. Many services reject passwords with spaces and various special characters. In some cases, the special characters that are not accepted might be an effort to avoid attacks like SQL injection that depend on those characters. But a properly hashed password would not be sent to a database intact, rendering such precautions unnecessary. Users should also be able to include space characters as to allow the use of phrases. Spaces themselves add little to password complexity and may introduce usability issues (e.g., the undetected use of two spaces rather than one), so it may be beneficial to remove repeated spaces in typed passwords prior to verification.

Users' password choices are very predictable, so attackers are likely to guess passwords that have been successful in the past. These include dictionary words and passwords from previous breaches, such as the "Password1!" example above. For this reason, it is recommended that passwords chosen by users be compared against a "black list" of unacceptable passwords. This list should include passwords from previous breach corpuses, dictionary words, and specific words (such as the name of the service itself) that users are likely to choose. Since users' password choice will also be governed by a minimum length requirement, this dictionary need only include entries meeting that requirement.

Highly complex memorized secrets introduce a new potential vulnerability: they are less likely to be memorable, and it is more likely that they will be written down or stored electronically in an unsafe manner. While these practices are not necessarily vulnerable, statistically some methods of recording such secrets will be. This is an additional motivation not to require excessively long or complex memorized secrets.

### A.4 Randomly-chosen Secrets

Another factor determining the strength of memorized secrets is the process by which they are generated. Secrets that are randomly chosen (in most cases by the verifier or CSP) and are uniformly distributed will be more difficult to guess or brute-force attack than user-chosen secrets meeting the same length and complexity requirements. Accordingly, at LOA2, SP 800-63-2 permitted the use of randomly generated PINs with 6 or more digits while requiring user-chosen memorized secrets to be a minimum of 8 characters long.

As discussed above, the threat model being addressed with memorized secret length requirements includes rate-limited online attacks, but not offline attacks. With this limitation, 6 digit randomly-generated PINs are still considered adequate for memorized secrets. 

### A.5 Summary

Length and complexity requirements beyond those recommended here significantly increase the difficulty of memorized secrets and increase user frustration. As a result, users often work around these restrictions in a counterproductive way. Further, other mitigations (such as blacklists, secure hashed storage, and rate limiting) are more effective at preventing modern brute-force attacks. Therefore, no additional complexity requirements are imposed.
