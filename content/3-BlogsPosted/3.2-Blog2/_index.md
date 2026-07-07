---
title: "Blog 2"
date: 2026-07-05
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---


# Creating great authentication experiences with Amazon Cognito and Authsignal

In modern digital applications, authentication is one of the most important parts of the user journey. Authentication protects user accounts, personal data, financial information, and other sensitive resources. However, strong security can sometimes create too much friction for users.

Many applications use multi-factor authentication, also known as MFA, to improve security. MFA can include SMS OTP, email OTP, authenticator apps, biometrics, passkeys, or hardware security keys. Although MFA increases protection, forcing users to complete MFA for every login or every action may create a poor user experience.

The AWS blog article **“Creating great authentication experiences with Amazon Cognito and Authsignal”** explains how Amazon Cognito and Authsignal can work together to create better authentication experiences. The main idea is to balance security and usability by using adaptive authentication, risk signals, continuous authentication, and flexible authentication methods.

Instead of applying the same authentication requirement to every user and every situation, the system can evaluate risk and apply the right level of authentication at the right time.

## 1. The challenge of authentication experience

Authentication has two goals that often compete with each other:

- Protect the application from unauthorized access.
- Keep the user experience simple and smooth.

If authentication is too weak, attackers may be able to access user accounts. If authentication is too strict, legitimate users may become frustrated and leave the application. For example, if a user must enter an OTP every time they open the application, the process may feel slow and repetitive.

This problem becomes more serious when an application grows. A large system may serve many users across many devices, locations, and usage patterns. Some login attempts are low risk, while others are suspicious. Treating every login attempt as equally risky can create unnecessary friction.

A better approach is to evaluate context. The system should ask:

- Is this a known device?
- Is the login location normal?
- Is the user behavior familiar?
- Is the action low risk or high risk?
- Is the transaction amount unusual?
- Is the user trying to access sensitive data?

By answering these questions, the system can decide whether the user should continue normally or complete an additional authentication step.

## 2. What is adaptive authentication?

Adaptive authentication is an authentication strategy that changes based on risk. Instead of requiring the same security step for every situation, the system analyzes context and decides what level of authentication is needed.

For example, if a user logs in from a trusted device, from a normal location, and during a usual time of day, the system may allow the login with minimal friction. However, if the same user logs in from a new device, from an unusual country, or at an abnormal time, the system may require MFA.

A simplified example:

```text
Low-risk login:
Known device + usual location + normal behavior
→ Allow access with low friction

High-risk login:
Unknown device + unusual location + abnormal behavior
→ Require additional authentication
```

This approach improves both security and user experience. Low-risk users are not interrupted unnecessarily, while high-risk situations receive stronger protection.

Adaptive authentication is especially useful for applications that need strong security but also care about user conversion, retention, and satisfaction.

## 3. Risk signals used in authentication

Risk signals are pieces of context that help the system understand whether an authentication attempt is normal or suspicious. These signals can come from the device, network, user behavior, transaction information, or application context.

Common risk signals include:

### Device signals

Device signals help determine whether the user is using a familiar device. The system may check browser fingerprint, device ID, operating system, browser type, or whether the device has been used before.

If a user logs in from a device that has been used many times before, the risk may be lower. If the user logs in from a completely new device, the system may treat the request as higher risk.

### Location signals

Location signals help identify unusual access patterns. For example, if a user logs in from Vietnam and then five minutes later logs in from another country far away, the system may detect this as suspicious.

This type of event is sometimes called impossible travel. It suggests that the account may be compromised or that one of the login attempts may not belong to the real user.

### Behavior signals

Behavior signals include login speed, login frequency, access time, navigation pattern, and other usage behavior. If a user normally logs in during office hours but suddenly signs in many times at midnight, the system may increase the risk score.

Behavior analysis helps the authentication system become more intelligent because it does not only check identity at one point in time. It also observes how users normally interact with the application.

### Transaction signals

Some actions are more sensitive than others. For example, viewing a public page may be low risk, but changing a password, adding a new payment method, or making a large transfer is high risk.

Transaction signals help the system decide whether step-up authentication is required. A normal transaction may continue without interruption, while a high-value or unusual transaction may require additional verification.

## 4. Continuous authentication beyond sign-in

A common mistake in authentication design is checking user identity only at sign-in. After the user logs in, the system may allow all actions without additional verification. This can be risky.

The article explains the idea of continuous authentication. This means the system can evaluate risk throughout the user session, not only at the beginning.

For low-risk actions, the user can continue normally. For sensitive or high-risk actions, the system can request stronger authentication.

Examples:

```text
Viewing general account information
→ No additional authentication required

Changing password
→ Require MFA or passkey verification

Adding a new payment method
→ Require additional authentication

Accessing sensitive data
→ Require stronger authentication

Making a high-value transaction
→ Require step-up authentication
```

This model improves security because the system can protect important actions even if the user has already signed in. It also improves user experience because the user is not challenged unnecessarily for every action.

## 5. Amazon Cognito as the identity foundation

Amazon Cognito is used to manage user authentication and identity in applications. It provides user pools, sign-up, sign-in, token-based authentication, and user management capabilities.

In an authentication architecture, Cognito can act as the identity foundation. It stores and manages user accounts, handles the initial login process, and issues tokens that applications can use to authorize requests.

Amazon Cognito is useful because it provides managed identity features without requiring the development team to build everything from scratch. Applications can integrate with Cognito for user registration, login, password reset, and secure session management.

However, authentication requirements are becoming more advanced. Many businesses need adaptive authentication, risk-based decisions, step-up authentication, and multiple authentication methods. This is where Authsignal can extend the authentication experience.

## 6. Authsignal as the risk and rules engine

Authsignal provides authentication orchestration and risk-based decision support. It can work with Amazon Cognito to help applications create adaptive and continuous authentication flows.

One important feature is the rules engine. A rules engine allows administrators to configure security rules based on context and business requirements. Instead of hardcoding all authentication logic in the application, the organization can define rules more flexibly.

For example, an administrator may create rules such as:

```text
If the user logs in from a new device
→ Require MFA

If the transaction amount is above a defined threshold
→ Require stronger authentication

If the user changes password
→ Require step-up authentication

If the user uses a trusted device and low-risk location
→ Allow low-friction access
```

This gives non-technical teams more flexibility because they can adjust security rules without requiring developers to change code every time.

Authsignal also supports different authentication methods. Depending on the risk level and user context, the system can choose methods such as OTP, passkeys, biometrics, or other verification options.

## 7. How Amazon Cognito and Authsignal work together

The combination of Amazon Cognito and Authsignal creates a stronger and more flexible authentication architecture.

A simplified flow can be described as:

```text
User action
→ Amazon Cognito handles identity and user session
→ Authsignal evaluates risk and business rules
→ The system decides the required authentication method
→ User completes the required verification if needed
→ Application allows or denies the action
```

Amazon Cognito manages the user identity layer, while Authsignal adds adaptive decision-making and authentication orchestration. This makes it possible to create a better balance between account security and user convenience.

This combination is useful because not every user action needs the same level of security. The system can remain simple for low-risk actions and become stricter for high-risk actions.

## 8. Authentication methods and user experience

A good authentication experience should provide several verification options. Different users and different regions may prefer different methods.

Common authentication methods include:

- SMS OTP
- Email OTP
- Authenticator app
- WhatsApp OTP
- Push notification
- Passkeys
- Biometrics
- Hardware security keys
- Liveness detection

Each method has advantages and disadvantages. SMS OTP is familiar, but it may be vulnerable to SIM swap attacks. Email OTP is easy to use, but it depends on email account security. Passkeys and biometrics can provide stronger protection and a smoother experience, but adoption may depend on device support and user familiarity.

The article highlights that authentication should not be static. Organizations should be able to adjust authentication methods based on risk, cost, and user needs.

For example, a business may choose WhatsApp OTP in some regions to reduce cost or improve delivery reliability. For high-risk actions, the system may require stronger methods such as passkeys, biometrics, or hardware keys.

![Blog 2](/images/3-Blog/Blog-2.png)

## 9. Benefits of adaptive and continuous authentication

Adaptive and continuous authentication provide several important benefits.

First, they reduce user friction. Users are not forced to complete MFA for every low-risk action. This makes the application easier to use and improves the overall experience.

Second, they improve security. The system can require stronger verification when risk is higher. This allows security to increase only when needed.

Third, they support business flexibility. Rules can be adjusted based on fraud patterns, user behavior, compliance needs, or business policies.

Fourth, they improve operational control. With a rules engine and authentication timeline, administrators can monitor authentication activity and update policies based on real-world usage.

Finally, they support better fraud prevention. Suspicious logins, unusual devices, abnormal locations, and high-risk transactions can trigger stronger verification automatically.

## 10. Main lessons from the article

The main lesson from this article is that authentication should not be designed as a fixed and static process. A good authentication experience must change based on user context, risk, and business requirements.

Important lessons include:

- Strong security should not always mean high friction.
- MFA should be applied intelligently, not blindly.
- Risk signals help the system decide when to challenge users.
- Authentication should continue after sign-in for sensitive actions.
- Amazon Cognito can provide the identity foundation.
- Authsignal can provide adaptive rules and authentication orchestration.
- Different authentication methods should be selected based on risk and user needs.
- A good authentication system must balance security, usability, cost, and flexibility.

## 11. Practical application

The ideas in this article can be applied to many applications that require both strong security and smooth user experience. Examples include healthcare applications, banking platforms, e-commerce systems, SaaS management platforms, and enterprise applications.

For low-risk actions, the application can allow users to continue without additional verification. For high-risk actions, the application can require stronger authentication. This creates a more balanced experience.

Instead of treating every user and every action the same way, adaptive authentication allows the system to make smarter decisions. This helps businesses reduce friction while still protecting sensitive actions and data.

Continuous authentication is also important because security should not stop after login. A user session may become risky later, especially if the user performs sensitive actions. Step-up authentication helps protect these moments.

## 12. Final thoughts

This article is useful because it shows that authentication design is not only about adding more security layers. It is about applying the right security layer at the right time.

A good authentication system should protect accounts without making every interaction difficult. Amazon Cognito and Authsignal can work together to support this goal by combining identity management, risk evaluation, rules-based decision-making, and flexible authentication methods.

Overall, the article provides a practical direction for building better authentication experiences. It shows that the best security experience is not always the strictest one, but the one that adapts to risk, user behavior, and business needs.

## Original Article

AWS Partner Network Blog:  
**Creating great authentication experiences with Amazon Cognito and Authsignal**

https://aws.amazon.com/blogs/apn/creating-great-authentication-experiences-with-amazon-cognito-and-authsignal/

## Discussion Question

Have you ever designed an authentication system that balances security and user experience? In your opinion, what is more challenging: reducing login friction for normal users or applying stronger protection for high-risk actions?