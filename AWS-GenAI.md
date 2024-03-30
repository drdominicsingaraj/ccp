# Generative-AI & AWS

## Machine Learning

Machine learning is a subfield of artificial intelligence (AI) that enables computers to learn from and make decisions based on data. Here's an overview of the concept:

### What is Machine Learning?

- **Definition**: Machine learning is the development of computer systems that can learn and adapt without following explicit instructions by using algorithms and statistical models to analyze and draw inferences from patterns in data.
- **Goal**: The aim is to allow machines to perform tasks requiring human intelligence, such as speech recognition, language translation, or decision-making.

### How Does it Work?

1. **Data Input**: Feed the machine learning algorithms with data.
2. **Learning**: The algorithms learn from the data by identifying patterns and features.
3. **Prediction**: Once trained, the algorithms can make predictions or decisions when presented with new data.

### Applications

- Machine learning is used in various applications, including recommendation systems, fraud detection, and more. It's a dynamic field that's continually expanding the capabilities of machines.

## Gen. AI from AWS's Perspective

Generative AI refers to machine learning models capable of generating new content or data that mirrors the training data but is not identical. AWS highlights Generative AI's potential to enhance productivity, create unique experiences, and foster rapid innovation across various sectors. AWS provides access to leading foundation models, enterprise-grade security, and privacy, enabling organizations to develop and scale Generative AI applications tailored to their specific data and use cases.

AWS's Generative AI services include:

- **SageMaker**: For building, training, and deploying machine learning models at scale.
- **Comprehend**: For natural language processing to uncover insights and relationships in text.
- **Rekognition**: For image and video analysis.

AWS is committed to responsible AI, ensuring that the AI solutions are ethical, transparent, fair, secure, and trustworthy. The investment in Generative AI by AWS is driving its development and application in diverse industries, including healthcare, financial services, and creative fields like advertising and marketing.

AWS offers a range of generative AI solutions designed to help businesses innovate faster and boost productivity. Here are some of the key offerings:

| AWS Generative Solutions | Description |
|--------------------------|-------------|
| **Amazon Bedrock** | A platform for building and scaling generative AI applications, offering access to foundation models like Anthropic's Claude 3 Haiku. |
| **Generative AI Application Builder** | Facilitates rapid development and deployment of generative AI applications, integrating with Amazon Bedrock and LLMs on Amazon SageMaker. |
| **AWS Inferentia2 Chips** | Used in Amazon EC2 Inf2 instances to reduce the cost of running generative AI workloads. |
| **AWS Trainium Chips** | Custom silicon designed for faster model training, available in Trn1n instances. |
| **Amazon CodeWhisperer** | Provides real-time coding assistance, now free for individual developers. |

These solutions incorporate security, privacy, and responsible AI practices, leveraging AWS's efficient and cost-effective infrastructure. For more information, visit the AWS Generative AI page.

## Amazon CodeWhisperer

AWS CodeWhisperer offers several advantages to enhance developer productivity and code quality:

| Benefit | Description |
|---------|-------------|
| **Increased Efficiency** | Generates code suggestions from snippets to full functions in real-time, based on comments and existing code. |
| **Expert Assistance** | Amazon Q, an interactive AI-powered assistant, provides expert guidance through a conversational interface within the IDE. |
| **Enhanced Security** | Identifies security vulnerabilities and offers code suggestions to remediate issues, ensuring code is secure by design. |
| **Multi-Language Support** | Works with 15 programming languages and various IDEs, fitting seamlessly into developers' workflows. |
| **Optimized for AWS** | Provides code suggestions optimized for AWS services, adhering to AWS best practices. |
| **Customizable Suggestions** | Can be customized to understand internal libraries, APIs, packages, classes, and methods, making recommendations more relevant. |
| **Developer Productivity** | In a productivity challenge, developers using CodeWhisperer completed tasks 27% more successfully and 57% faster on average. |

### Configure AWS CodeWhisperer in Visual Studio Code

To set up AWS CodeWhisperer in Visual Studio Code, follow these steps:

1. **Launch Visual Studio Code**.
   - Open Visual Studio Code on your machine.

2. **Install the AWS Toolkit**.
   - Go to the Extensions marketplace in Visual Studio Code.
   - Search for and install the **AWS Toolkit for Visual Studio Code**.

3. **Open the AWS Toolkit**.
   - Access the AWS Toolkit from the Visual Studio Code sidebar.

4. **Authenticate with AWS**.
   - Use your AWS credentials to authenticate.
   - This can be done through AWS IAM credentials or AWS Builder ID.

5. **Enable CodeWhisperer**.
   - Find CodeWhisperer settings within the AWS Toolkit preferences.
   - Ensure that CodeWhisperer is enabled.

For more detailed instructions, consult the official AWS documentation or the AWS Toolkit for Visual Studio Code user guide.

![Code Whisperer](images/CodeWhisperer.png)

### Using AWS CodeWhisperer in Visual Studio Code

- **Write or Open a Code File**: Create a new file or open an existing project in a supported language.
- **Start Typing Code**: Begin coding as you normally would. CodeWhisperer should offer suggestions in real-time.
- **Accept Suggestions**: When you see a suggestion that fits your needs, use `Tab` or `Enter` to accept it.
- **Trigger Suggestions Manually**: If you want to invoke CodeWhisperer manually, you can use the shortcut `Ctrl + Space` (or `Cmd + Space` on macOS) to trigger suggestions.
- **Review Suggestions**: Evaluate the relevance and accuracy of the suggestions to your coding context.
- **Check for Updates**: Ensure that the language server, which powers CodeWhisperer’s suggestions, is up-to-date. The AWS Toolkit should handle this automatically.

___

### Improving Developer Productivity with Amazon CodeWhisperer at Accenture

Accenture has integrated Amazon CodeWhisperer into their software engineering best practices, particularly within their Velocity platform. Balakrishnan Viswanathan, Senior Manager of Tech Architecture at Accenture, highlights the impact of this integration:

"**Accenture is using Amazon CodeWhisperer to accelerate coding as part of our software engineering best practices initiative in our Velocity platform**," says Viswanathan. "**The Velocity team was looking for ways to improve developer productivity. After searching for multiple options, we came across Amazon CodeWhisperer to reduce our development efforts by up to 30% and we are now focusing more on improving security, quality, and performance.**"

### Benefits of CodeWhisperer from Accenture point of view

The Accenture Velocity team has been utilizing CodeWhisperer to enhance their artificial intelligence (AI) and machine learning (ML) projects. The benefits they've observed include:

- **Efficiency**: The team spends less time on boilerplate and repetitive code patterns, allowing more focus on building high-quality software.
- **Empowerment**: CodeWhisperer enables developers to use AI responsibly to create syntactically correct and secure applications.
- **Function Generation**: Developers can generate entire functions and logical code blocks without the need to search for and customize snippets from the web.
- **Accelerated Onboarding**: The tool helps to speed up the onboarding process for novice developers or those working with an unfamiliar codebase.
- **Enhanced Security**: Security threats are detected early in the development process by integrating security scanning into the developer’s IDE.

```markdown
[How Accenture is Using Amazon CodeWhisperer to Improve Developer Productivity](https://aws.amazon.com/blogs/machine-learning/how-accenture-is-using-amazon-codewhisperer-to-improve-developer-productivity/)
```

### 10 Ways to Build Applications Faster with Amazon CodeWhisperer

1. **Typing Less**: Reduce the amount of manual coding by leveraging CodeWhisperer's ability to understand and generate code.
2. **Generating Functions Using Code**: Automatically generate functions based on the code you've already written.
3. **Generating Functions Using Comments**: Use natural language comments to guide CodeWhisperer in creating functions that match your specifications.
4. **Generating Classes**: Quickly create new classes with CodeWhisperer's assistance, speeding up the development of complex structures.
5. **Implementing Algorithms**: Implement algorithms efficiently with CodeWhisperer's help, saving time on problem-solving and coding.
6. **Writing Unit Tests**: Generate unit tests automatically to ensure your code works as intended, leading to a more reliable application.
7. **Creating Sample Data**: Easily create sample data for testing and development purposes.
8. **Simplifying Regular Expressions**: Simplify the creation and understanding of complex regular expressions with CodeWhisperer's guidance.
9. **Learning Third-Party Code Libraries Faster**: Accelerate the learning curve for new libraries by using CodeWhisperer to provide examples and explanations.
10. **Documenting Code**: Improve code documentation with CodeWhisperer's ability to generate comments and explanations for your code.

```markdown
[10 Ways to Build Applications Faster with Amazon CodeWhisperer](https://aws.amazon.com/blogs/devops/10-ways-to-build-applications-faster-with-amazon-codewhisperer/)
```

___

This strategic move aims to enhance the efficiency of Accenture's development process, allowing the team to devote more attention to critical aspects such as security, quality, and performance.

## Amazon Q

Amazon Q is a generative AI-powered assistant designed for business use. It's part of the AWS (Amazon Web Services) and allows users to create chat applications that can answer questions, provide summaries, generate content, and complete tasks based on data within an enterprise. It integrates with services like Amazon Kendra, S3, SharePoint, and Salesforce, and offers configurable access and security settings to ensure that responses are generated using authorized enterprise data. Currently, Amazon Q is in preview release.

### Usage Examples of Amazon Q

1. **Marketing Management**: A marketing manager could use Amazon Q to transform a press release into a blog post, create a summary of the press release, or draft an email based on the release. Amazon Q can also generate tailored social media prompts to promote stories through various channels.

2. **Business Analysis**: Business analysts might employ Amazon Q to gain quicker, easier data insights by asking it to summarize key points from data reports or visualize data trends.

3. **Supply Chain Management**: For supply chain queries, Amazon Q could analyze a company's supply chain and provide suggestions for improvements. For instance, it might suggest alternative shipping routes to avoid delays caused by unforeseen events like weather conditions.

4. **Healthcare Data Analysis**: In the healthcare sector, companies like Gilead Sciences use Amazon Q for faster analysis of extensive data, which can help in making informed decisions.

### Setting Up Amazon Q

Setting up Amazon Q involves several steps to ensure proper integration with your AWS account and development environment. Below is a summary of the process:

### Initial Setup

1. **AWS Account**: Create an AWS account by signing up on the AWS website and completing the verification process.

2. **Secure Root User**: Secure your root user with multi-factor authentication (MFA) and create an administrative user for everyday tasks.

3. **Enable IAM Identity Center**: Manage identities and grant administrative access to users within your organization.

4. **AWS CLI**: Install the AWS Command Line Interface to manage your AWS services.

5. **AWS SDKs**: Download and install the AWS SDKs for use with Amazon Q.

<!-- Configuration -->
### Configuration

6. **AWS Regions and Endpoints**: Select the AWS Region that fits your needs and set up the necessary endpoints for Amazon Q.

7. **Permissions**: Assign the necessary permissions to use Amazon Q within your AWS account.

8. **AWS Toolkit**: Install the AWS Toolkit in your IDE, available as an extension in Visual Studio Code and JetBrains.

9. **Authenticate**: Authenticate Amazon Q through IAM Identity Center or AWS Builder ID after installing the AWS Toolkit.

For detailed instructions, refer to the official Amazon Q documentation.

![Amazon Q](images/AmazonQ.png)
