## Functions in Shell Scripting

Organizing code using functions improves clarity and efficiency. Functions encapsulate specific logic, such as:

    Checking script arguments

        Example: check_num_of_args() validates if the script received the correct number of arguments.

        Syntax:
``` bash

    check_num_of_args() {
      if [ "$#" -ne 1 ]; then
        echo "Usage: $0 <environment>"
        exit 1
      fi
    }
```
Verifying AWS CLI installation

    Example: check_aws_cli() uses command -v aws to check if AWS CLI is installed.

    Redirects output to /dev/null to suppress errors.

    Syntax:
``` bash

    check_aws_cli() {
      if ! command -v aws &>/dev/null; then
        echo "AWS CLI not installed. Please install it."
        return 1
      fi
    }
```
Validating AWS authentication

    Example: check_aws_profile() checks if $AWS_PROFILE is set.

    Uses -z to test for empty variables.

    Syntax:
``` bash

    check_aws_profile() {
      if [ -z "$AWS_PROFILE" ]; then
        echo "AWS_PROFILE environment variable not set."
        return 1
      fi
    }
``` 
Environment-based logic

    Example: activate_infra_environment() executes commands based on the argument (local, testing, or production).

    Syntax:
``` bash

        activate_infra_environment() {
          case "$ENVIRONMENT" in
            local)    echo "Running for Local Environment..." ;;
            testing)  echo "Running for Testing Environment..." ;;
            production) echo "Running for Production Environment..." ;;
            *) echo "Invalid environment. Use 'local', 'testing', or 'production'."; exit 2 ;;
          esac
        }
```
AWS Configuration Files

    ~/.aws/credentials: Stores AWS keys (e.g., aws_access_key_id, aws_secret_access_key) for different profiles (e.g., default, testing, production).

    ~/.aws/config: Defines regions and output formats for profiles.

Script Structure

    Define environment variables (e.g., ENVIRONMENT=$1).

    Declare functions (e.g., check_num_of_args, check_aws_cli).

    Call functions in sequence at the end of the script.

Key Notes

    Functions are inactive until called.

    Use return 1 for error conditions.

    Redirect output (&>/dev/null) to silence commands.

    Always validate inputs and dependencies.

Summary

The guide demonstrates modular shell scripting for AWS automation, emphasizing function usage for argument checks, dependency validation, and environment-specific actions. It highlights AWS configuration files (credentials and config) and advocates a structured approach—defining variables, functions, and function calls—to ensure maintainability.