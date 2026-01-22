# password-strength-analyzer
Cybersecurity tool - password strength checker with Python + Web UI
#!/usr/bin/env python3
import re
import string
from datetime import datetime

print("💰 PAID PROJECT: Password Strength Analyzer")
print("=" * 60)

def analyze_password(password):
    score = 0
    issues = []
    
    # Length
    if len(password) >= 12: score += 30
    elif len(password) >= 8: score += 20
    else: issues.append("❌ Too short")
    
    # Character types
    has_upper = bool(re.search('[A-Z]', password))
    has_lower = bool(re.search('[a-z]', password))
    has_digit = bool(re.search('[0-9]', password))
    has_special = bool(re.search(f'[{re.escape(string.punctuation)}]', password))
    
    if has_upper: score += 15 else: issues.append("❌ No UPPERCASE")
    if has_lower: score += 15 else: issues.append("❌ No lowercase") 
    if has_digit: score += 20 else: issues.append("❌ No numbers")
    if has_special: score += 20 else: issues.append("❌ No special chars")
    
    strength = "WEAK" if score < 40 else "STRONG" if score < 70 else "VERY STRONG"
    
    return {'score': score, 'strength': strength, 'issues': issues}

# Test
test_passwords = ["123456", "Password123!", "MyStr0ngP@ss2026"]
for pwd in test_passwords:
    result = analyze_password(pwd)
    print(f"\n{pwd}: {result['strength']} ({result['score']}/100)")
    print(f"Issues: {', '.join(result['issues'])}")
