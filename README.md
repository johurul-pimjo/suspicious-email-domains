# Suspicious Email Domains

A curated list of suspicious email domains commonly associated with spam, phishing, or fraudulent activities. This repository provides a simple way to check if an email domain is potentially suspicious.

## Features

- **Comprehensive List**: Contains thousands of known suspicious domains.
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

## Data Sources

The domains are collected from various sources including:

- Public reports of spam and phishing domains
- Community contributions
- Automated scans and monitoring

## Contributing

Contributions are welcome! If you know of suspicious domains not listed here, please:

1. Fork the repository
2. Add the domains to the appropriate files
3. Submit a pull request

## Files

- `domains.txt`: Plain text list of domains (one per line)
- `domains.json`: JSON array of domains
- `domains.csv`: CSV format with domains
- `merge_domains.js`: Script to merge and process domains

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Disclaimer

This list is not exhaustive and should be used as one of many tools in email validation. Always combine with other security measures.
