Scenario-1
1. Create a Compliance Policy.
2. Configure the compliance action/status as **Non-Compliant**.
3. Add a compliance criterion:
    - Property: **Intended Purposes**
    - Value: **Signing And Encryption**
4. Save the policy.
5. Assign the compliance policy to a device that contains a certificate configured with **Signing And Encryption** as its Intended Purpose.
Scenario-2
- Disable SOTI search and test the various search functionality against any device
Scenario-3
- Right click on Device Group
- Select **Apple** Family
- Select **Shared iPad For Business**
- Try adding few valid and invalid domains that satisfy the regex `^(\*|[a-zA-Z0-9]([a-zA-Z0-9\-]{0,61}[a-zA-Z0-9])?)\.([a-zA-Z0-9]([a-zA-Z0-9\-]{0,61}[a-zA-Z0-9])?\.)*[a-zA-Z]{2,63}(\/[^\/]+)*$`