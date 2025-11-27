# Suspicious and Disposable Email Domains

A curated list of suspicious and disposable email domains commonly associated with spam, phishing, or fraudulent activities. This repository provides a simple way to check if an email domain is potentially suspicious or disposable.

## Features

- **Comprehensive List**: Contains thousands of known suspicious and disposable domains.
- **Easy Integration**: Use the provided JavaScript function to check domains programmatically.
- **Open Source**: Community-driven and regularly updated.

## Usage

You can fetch the list of domains directly from this repository and use it in your applications to validate email domains.

### JavaScript Example

Here's a simple JavaScript function to check if an email domain is in the suspicious list:

```javascript
export const checkEmailDomain = async (email) => {
  try {
    const res = await fetch(
      "https://raw.githubusercontent.com/said7388/suspicious-email-domains/refs/heads/main/domains.txt",
    );

    if (!res.ok) {
      return false;
    }

    const content = await res.text();
    const blocklist = content.split("\n").slice(0, -1);
    // Check if the email domain is in the blocklist
    const mailDomain = email.split("@")[1];
    const findIndex = blocklist.findIndex((item) => item === mailDomain);

    return findIndex !== -1;
  } catch (_error) {
    // console.log(error);
    return false;
  }
};
```

### How to Use

1. Call the `checkEmailDomain` function with an email address.
2. It returns `true` if the domain is suspicious, `false` otherwise.

Example:

```javascript
const isSuspicious = await checkEmailDomain("user@0-00.usa.cc");
console.log(isSuspicious); // true
```

### JSON Example (JavaScript)

Here's a JavaScript function using the JSON format:

```javascript
export const checkEmailDomainJson = async (email) => {
  try {
    const res = await fetch(
      "https://raw.githubusercontent.com/said7388/suspicious-email-domains/refs/heads/main/domains.json",
    );

    if (!res.ok) {
      return false;
    }

    const blocklist = await res.json();
    const mailDomain = email.split("@")[1];
    return blocklist.includes(mailDomain);
  } catch (_error) {
    return false;
  }
};
```

### PHP Example

Here's a PHP function to check the email domain:

```php
function checkEmailDomain($email) {
    try {
        $url = "https://raw.githubusercontent.com/said7388/suspicious-email-domains/refs/heads/main/domains.json";
        $json = file_get_contents($url);
        if ($json === false) {
            return false;
        }
        $blocklist = json_decode($json, true);
        if ($blocklist === null) {
            return false;
        }
        $mailDomain = explode('@', $email)[1];
        return in_array($mailDomain, $blocklist);
    } catch (Exception $e) {
        return false;
    }
}
```

### Python Example

Here's a Python function to check the email domain:

```python
import requests

def check_email_domain(email):
    try:
        url = "https://raw.githubusercontent.com/said7388/suspicious-email-domains/refs/heads/main/domains.json"
        response = requests.get(url)
        if not response.ok:
            return False
        blocklist = response.json()
        mail_domain = email.split('@')[1]
        return mail_domain in blocklist
    except:
        return False
```

### Go Example

Here's a Go function to check the email domain:

```go
package main

import (
    "encoding/json"
    "net/http"
    "strings"
)

func checkEmailDomain(email string) bool {
    url := "https://raw.githubusercontent.com/said7388/suspicious-email-domains/refs/heads/main/domains.json"
    resp, err := http.Get(url)
    if err != nil {
        return false
    }
    defer resp.Body.Close()
    if resp.StatusCode != http.StatusOK {
        return false
    }
    var blocklist []string
    if err := json.NewDecoder(resp.Body).Decode(&blocklist); err != nil {
        return false
    }
    mailDomain := strings.Split(email, "@")[1]
    for _, domain := range blocklist {
        if domain == mailDomain {
            return true
        }
    }
    return false
}
```

## Data Sources

The domains are collected from various sources including:

- Public reports of spam and phishing domains
- Lists of disposable email services
- Community contributions
- Automated scans and monitoring

## Contributing

Contributions are welcome! If you know of suspicious domains not listed here, please:

1. Fork the repository
2. Add the domains to the appropriate files
3. Submit a pull request

## Files

- `domains.txt`: Plain text list of suspicious and disposable domains (one per line)
- `domains.json`: JSON array of suspicious and disposable domains
- `domains.csv`: CSV format with suspicious and disposable domains
- `merge_domains.js`: Script to merge and process domains

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Disclaimer

This list of suspicious and disposable domains is not exhaustive and should be used as one of many tools in email validation. Always combine with other security measures.
