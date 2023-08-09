# Codebase Guidelines

These guidelines aim to establish a consistent and efficient approach to code development within our project groups. By adhering to these guidelines, we can foster enhanced collaboration, uphold code quality, and guarantee a seamless workflow. Kindly review and follow the guidelines outlined below.

Your commitment to these guidelines is pivotal to the project's success. Should you have queries or require further details, please reach out. Wishing you a productive coding experience!

## **Archiving**
- **Definition:** Clearly specify what aspects of the codebase are being archived.
- **Utility Over Features:** Give precedence to utilities over specific tasks or features.
- **Function Structure:** Advocate for an orthogonal arrangement of functions.
- **Circular References:** Refrain from creating utility libraries susceptible to circular references.

## **Version Control (Git)**
- **Tool:** Employ Git for version control. [Visit our repository](https://github.com/cmu-mfi/).
- **Branching:** Highlight the importance of branching for effective teamwork and code administration.
- **Additional Tips:** Explore more git tips.

## **Platform and Language Preferences**
- **Operating System:** While Linux is the preferred choice, it's not obligatory.
- **Programming Languages:** C++ and Python are favored, but not compulsory.

## **Style Guide**
- **Magic Numbers:** Steer clear of magic numbers in the code.
- **Naming Conventions:** Maintain uniformity in naming with `CamelCase` for classes and `snake_case` for variables and functions.
- **Descriptiveness:** Ensure variable and function names are both descriptive and succinct.
- **Utility Prefix:** For utility functions, consider prefixing with the scope. For instance, string manipulation functions might be `str_<utility>`.
- **Headers:** Incorporate appropriate file and function headers, such as:
  ```c++
  /*
  * @brief - Purpose and functionality of the function
  * @params[in] - Input parameters and a brief description 
  * @params[out] - Outputs of the function (mention if none and describe any internal modifications)
  */

## **Comments**
- **Complex Sections:** Provide comments for intricate code segments or nuanced formulas to aid comprehension.
- **Minimize Specificity:** Limit line-specific comments unless absolutely essential.
- **Clean-Up:** Excise dead code and superfluous print statements prior to the final submission.
- **Indentation:** Utilize indentation to augment code readability and clarify control flow.


<!-- 
We welcome and appreciate contributions from the community! This document provides guidance for individuals interested in contributing to our codebase.

## How to Contribute

1. **Fork and clone**: Start by forking the project to your personal GitHub account. After that, clone the repository on your local machine to start making your changes.

2. **Make your changes**: Make the changes you think would improve the codebase. This could be fixing a bug, adding a new feature, optimizing existing code, improving documentation, etc.

3. **Test your changes**: Before submitting your changes, please make sure to test them thoroughly. We strive to maintain high-quality, reliable code, and your testing helps ensure this!

4. **Commit your changes**: Make a commit with a meaningful commit message describing what you've done.

5. **Submit a pull request**: Push your changes to your forked repository on GitHub, then submit a pull request against the main repository.

## Coding Guidelines

- Please ensure your code follows the coding style used throughout the existing codebase.
- Include comments in your code where necessary.
- Ensure your code is free of errors and warnings.

## Pull Requests

- Each pull request should contain only one feature or fix. If you have made multiple changes, please make separate pull requests for each of them.
- Pull requests should be created against the `master` branch.
- Include relevant issue numbers (if any) in the pull request description.
- All pull requests are subject to review and approval by the project maintainers.

## Issues

- Feel free to submit issues regarding bugs, feature requests, and enhancements.
- Include a detailed description so that we can understand and reproduce the issue. If possible, include steps to reproduce, expected behavior, and actual behavior.

## Community

Remember that this is a community effort. Be respectful and professional in all your interactions. We are all here to help each other and make this codebase the best it can be!

Thank you for your interest in contributing to our codebase! We look forward to your collaboration.

**Note:** By submitting a pull request, you agree to license your contributions under the same license as this project.
-->
[**Go to Main Page**](https://github.com/cmu-mfi/)
