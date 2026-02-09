## Test Functions Explained Simply

This is a **test file** — think of it like a quality checker. It tests whether the notification builder (from the previous file) works correctly. Here's what each function does:

---

### **Setup & Preparation Functions**

**`setUp()` (Runs before every test)**
- Like preparing a test kitchen before each cooking test
- Creates fresh tools/equipment for each test
- Disables the feature flag by default (sets it to "off")

**`setupFeatureFlagEnabled()`**
- Flips a switch to turn the feature flag "on"
- Used when tests need detailed lead scoring information

**`createBaseFormFill()`, `createFormFillWithMessage()`, `createFormFillWithKeyInfo()`**
- Factory functions that build test data
- Like having template forms ready to use
- Saves time instead of creating data from scratch each time

**`createElement()`**
- Creates a test field with a label and value
- Example: creates `"Company: Acme Corp"`

---

### **Basic Form Type Tests** *(Checking different form sources)*

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFillForSocial()` | Social media form submissions work correctly |
| `testBuildFormFillForSearch()` | Search query forms work correctly |
| `testBuildFormFillForWebsite()` | Website contact forms work correctly |
| `testBuildFormFillForTextLead()` | Text message/SMS forms work correctly |

**What they verify:** Each form type shows the right message title and includes the correct information.

---

### **Feature Flag Tests** *(Testing with detailed scoring enabled)*

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFill_SocialLead_WithFeatureFlagEnabled()` | Social forms with scoring details |
| `testBuildFormFill_SearchLead_WithFeatureFlagEnabled()` | Search forms with scoring details |
| `testBuildFormFill_WebsiteFormFill_WithFeatureFlagEnabled()` | Website forms with scoring details |
| `testBuildFormFill_TextLead_WithFeatureFlagEnabled()` | Text forms with scoring details |

**What they verify:** When the feature is turned on, the message includes "Lead score: Quality/Potential/Spam" information.

---

### **Lead Quality/Category Tests**

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFill_LeadCategory_Lead()` | High-quality leads show "Quality" |
| `testBuildFormFill_LeadCategory_PotentialLead()` | Medium leads show "Potential" |
| `testBuildFormFill_LeadCategory_NonLead()` | Spam shows "Suspected Spam" |
| `testBuildFormFill_LeadCategory_Unknown()` | Unknown types show "Unscored" |
| `testBuildFormFill_LeadCategory_CaseInsensitive()` | "LEAD", "Lead", "lead" all work the same |

**What they verify:** Leads are correctly rated with the right quality label.

---

### **Null/Missing Data Tests** *(Handling missing information gracefully)*

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFill_NullMessage()` | Works when message object is missing |
| `testBuildFormFill_EmptyName()` | Works when name field is blank |
| `testBuildFormFill_NullEmail()` | Works when email is missing |
| `testBuildFormFill_NullPhone()` | Works when phone is missing |
| `testBuildFormFill_NullOptionalFields()` | Works when optional fields are missing |
| `testBuildFormFill_EmptyOptionalFields()` | Works when optional fields list is empty |
| `testBuildFormFill_NullCallerLocation()` | Works when location isn't provided |
| `testBuildFormFill_EmptyCallerLocation()` | Works when location is blank |

**What they verify:** The notification builder **doesn't crash** when data is missing—it just skips that field.

---

### **Location/URL Tests**

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFill_NullFormFillKeyInfo()` | Works if key info object is missing |
| `testBuildFormFill_NullLocationId()` | Works if location ID is null |
| `testBuildFormFill_EmptyLocationId()` | Works if location ID is empty |
| `testBuildFormFill_PlatformTrue_WithLocationId()` | Creates proper dashboard URL with location |
| `testBuildFormFill_PlatformTrue_NullLocationId()` | Creates basic dashboard URL without location |
| `testBuildFormFill_PlatformFalse()` | Creates generic leads URL |

**What they verify:** The clickable link sends users to the right dashboard page, even if location info is missing.

---

### **Form Elements/Fields Tests**

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFill_Elements_LocationIdSkipped()` | Hides "Location ID" field (filtered out) |
| `testBuildFormFill_Elements_LabelWithColon()` | Handles labels that end with `:` |
| `testBuildFormFill_Elements_LabelWithWhitespace()` | Cleans up extra spaces in labels |
| `testBuildFormFill_Elements_MessageLabel()` | Correctly places message fields |
| `testBuildFormFill_Elements_NameEmailPhoneFiltered()` | Filters out primary fields from extra data |
| `testBuildFormFill_Elements_EmptyContent()` | Works with single fields |
| `testBuildFormFill_Elements_Multiple()` | Handles multiple extra fields correctly |

**What they verify:** Custom form fields are formatted and included properly in the notification.

---

### **Text Lead/Texter Name Tests**

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFill_TextLead_TexterNamePresent()` | Shows who sent the text message |
| `testBuildFormFill_TextLead_TexterNameNull()` | Works when texter name is missing |
| `testBuildFormFill_TextLead_TexterNameEmpty()` | Works when texter name is blank |
| `testBuildFormFill_TextLead_WithCallerLocation()` | Includes location for text leads |
| `testBuildFormFill_TextLead_TitleWithFeatureFlag()` | Shows "New Hibu Lead (Text)" title |
| `testBuildFormFill_TextLead_BodyFormatNoFeatureFlag()` | Shows simple format without scoring |

**What they verify:** Text message notifications format correctly with or without sender information.

---

### **Phone Number Tests**

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFill_PhoneNumber_Valid()` | Normal phone numbers work |
| `testBuildFormFill_PhoneNumber_Null()` | Missing phone is handled gracefully |
| `testBuildFormFill_PhoneNumber_Empty()` | Blank phone is handled gracefully |
| `testBuildFormFill_PhoneNumber_SpecialCharacters()` | Formatted numbers like "(123) 456-7890" work |

**What they verify:** Phone numbers are properly formatted no matter the format they come in.

---

### **Edge Case Tests** *(Unusual or extreme scenarios)*

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFill_EdgeCase_LongFieldValues()` | Very long messages (500+ characters) |
| `testBuildFormFill_EdgeCase_SpecialCharacters()` | Symbols like `& < > !` in data |
| `testBuildFormFill_EdgeCase_UnicodeCharacters()` | Foreign languages (Chinese, Spanish) |
| `testBuildFormFill_EdgeCase_FormfillStringCase()` | "SearchLead", "SEARCHLEAD" all work |
| `testBuildFormFill_EdgeCase_NullBusinessId()` | Missing business ID is handled |

**What they verify:** The builder works with unusual/extreme data without breaking.

---

### **Final Output Tests**

| Test Name | What it checks |
|-----------|---|
| `testBuildFormFill_ActionCreated()` | The button ("Open Dashboard") is created |
| `testBuildFormFill_UrlAlwaysSet()` | The clickable link is always included |

**What they verify:** The final notification always has a button and link, even in edge cases.

---

## Summary in One Sentence

**These tests are quality checkers that verify the notification builder handles every possible scenario correctly—including when data is missing, weird, or unusual.**
