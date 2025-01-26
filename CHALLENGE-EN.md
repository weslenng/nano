# Back-End Programming Challenge

⚠️ This is an AI translation, please check the [original file](CHALLENGE.md) for accuracy.

Hello and thank you very much for your interest in UmHelp! We are a fast-growing
startup, and we are always looking for good people to join our technology
team. We hope to have you on board with us soon!

We ask that you read this document **entirely** carefully to maximize your
chances of success.

The test you will perform consists of developing a server for registering
accounts and financial transactions. This system must be able to receive multiple
transaction requests simultaneously, persistently record the transaction history,
and return the current balance of each account.

## About this document
- The process of submitting your solution and the criteria that will be evaluated by
UmHelp's technology team are described below in the **Evaluation** section.
- The interface that must be exposed by the server is described in the **Interface** section.
- The rules that the system must follow are described in the **Business
Rules** section.
- The interface descriptions occasionally reference entities described in the **Entities** section.

If you are unsure about anything explained in this document (or
have any questions in general), feel free to send an email to
tech@umhelp.com with your questions.

## Evaluation
Your challenge should be made available through a Git repository
(which can be hosted in whatever way is most convenient for you, for
example using a platform like GitHub or GitLab). The only restriction is that
the repository must be accessible to the UmHelp team. If you don't want to
make your code publicly available, talk to us about how we can
get access to your code.

### Criteria
Once it is made available to us, your code will be evaluated according to the following criteria, in approximate order of importance:

#### Absence of bugs
Your code must work correctly, meeting all the requirements of the specification represented by this document

#### Readability and Formatting
Remember that a piece of code will generally be read many more times than
written. Write your code thinking about who will read it. Seek to minimize
reading difficulties. Use indentation to your advantage. Follow good code
formatting practices of the chosen language.

#### Clarity
Your code should make your intention clear to the reader. As much as
plausible, it should be possible to understand what the code does just by reading it.
Explanations using comments should be redundant.

#### Decoupling
Your code should not create unnecessary dependencies between modules.
When changing one part of the code, it should not be necessary to change parts without
logical relation to the changed part.

#### Extensibility
Although this challenge is only theoretical, try to consider the code you
will develop as if it were going to be just part of a larger solution. Think
about the effort required to make additions to your code and seek to
minimize it.

#### Maintainability
Write your code as if it were going to be maintained for a long time after you
create it, by various people with varying levels of experience. Think about the
effort required to change your code and seek to minimize it. If I want to change just one aspect of the code, how many parts of it will I need to change?

#### Optional
The following points are optional, but we appreciate seeing them:
- Unit and integration tests
- System deployed on some cloud provider
- Well-structured validations and errors

#### After the technical challenge
In general, we will evaluate your code a few days after submission. Once our
evaluation is complete, we will send feedback about your solution. If
your code is approved, in addition to the feedback, we will set a date for an
in-person interview or a video call conversation with you.

#### In-person interview
In the in-person interview, we will talk with you about the structure of your code and the choices you made. Be ready to explain the decisions you made and discuss alternatives. Some topics we will touch on (but not the only ones) will be: choice of databases, interface structures, code architecture. Additionally, we may change the conditions of the challenge and ask what you would have done differently.

## Interface
The server interface can be implemented using the API pattern of the
candidate's choice (some examples are REST, GraphQL, and gRPC patterns), as long as it adheres to the
requirements specified here.

### Endpoints
Regardless of the technology chosen to implement the API, it must expose
endpoints allowing the operations described below.

#### Account registration
In this endpoint, account data should be sent and it should be registered in the account database, if the user data is valid according to the **Business Rules** section.

#### Authentication
In this endpoint, login data for an already registered account should be sent.
This data should be validated and a token should be returned that will be used
to validate user transactions. In the next endpoints, the token must be
sent to identify the logged-in user.

#### Transaction registration
In this endpoint, transaction data should be sent and it should be
registered in the transaction database, if it is made between valid accounts and
if there is sufficient balance in the logged-in user's account to complete it.

#### Transaction reversal
In this endpoint, the ID of an already registered transaction should be sent and the effects of this transaction should be reversed, if possible and if the transaction was initiated by the logged-in user.

#### Transaction search by date
In this endpoint, start and end dates should be sent.
The endpoint should return all transactions made by the logged-in user between these dates in chronological order.

#### Balance view
In this endpoint, the logged-in user's balance should be viewed.

## Business Rules
1. A transaction should only be carried out if there is sufficient balance in the user's account to complete it.
2. After a transaction is completed, the sending user's account should have its value reduced by the transaction amount and the receiving user's account should be increased by the transaction amount.
3. All transactions performed must be recorded in the database.
4. If all transactions in the database are performed again from the initial state of all accounts, the balances should equal the balances exposed in the interface.

## Entities
The entities described below are specifications of the minimum data necessary for system operations. Other fields can be added as the candidate considers necessary.

### User Account
A user account needs at minimum the following data for creation:

- First and last name of the holder
- Holder's CPF (Brazilian ID number)
- Initial balance

Additionally, the account must store at minimum the following data:

- Unique identifier
- Creation date

### Transaction
A transaction needs at minimum the following data for creation:

- Sender account identifier
- Receiver account identifier
- Amount

Additionally, the record must contain at minimum the following data:

- Processing date
- Unique identifier
