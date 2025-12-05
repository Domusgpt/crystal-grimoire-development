# Crystal Grimoire - Comprehensive Upgrade Plan

**Created:** December 5, 2025
**Status:** Planning Document
**Total Items:** 127 tasks across 8 major categories

---

## Executive Summary

This document outlines all required upgrades, fixes, and enhancements for Crystal Grimoire. Each section contains checkboxes for tracking completion.

---

## Table of Contents

1. [Crystal Database Enhancement](#1-crystal-database-enhancement)
2. [AI Model Migration (Gemini 2.5 Flash Lite)](#2-ai-model-migration)
3. [Marketplace Functionality](#3-marketplace-functionality)
4. [Collections & Journal Fixes](#4-collections--journal-fixes)
5. [Home Screen UI Redesign](#5-home-screen-ui-redesign)
6. [Settings & Configuration Fixes](#6-settings--configuration-fixes)
7. [Code Quality & Technical Debt](#7-code-quality--technical-debt)
8. [Authentication & Security](#8-authentication--security)

---

## 1. Crystal Database Enhancement

### Priority: HIGH | Estimated Tasks: 25

The crystal database needs comprehensive enhancement with real photos and expanded metaphysical data.

### 1.1 Create Comprehensive Crystal Database File

**File to Create:** `/lib/data/crystal_database.dart`

- [ ] **1.1.1** Create `CrystalDatabase` class with static crystal data
- [ ] **1.1.2** Define `CrystalData` model with all metaphysical fields
- [ ] **1.1.3** Populate with 50+ common crystals initially

### 1.2 Required Metadata Fields Per Crystal

Each crystal entry must include:

```dart
class CrystalData {
  // Basic Information
  String id;
  String name;
  String scientificName;
  String crystalFamily;
  List<String> aliases;

  // Physical Properties
  String color;
  String colorDescription;
  double hardness;           // Mohs scale (1-10)
  String crystalSystem;      // cubic, hexagonal, etc.
  String luster;             // vitreous, metallic, etc.
  String transparency;       // transparent, translucent, opaque
  String rarity;             // common, uncommon, rare, very rare

  // Metaphysical Properties
  List<String> chakras;      // root, sacral, solar_plexus, heart, throat, third_eye, crown
  List<String> zodiacSigns;  // aries, taurus, gemini, etc.
  List<String> birthSigns;   // Month associations
  List<String> elements;     // earth, water, fire, air, spirit
  List<String> planetaryRulers;
  String energyType;         // grounding, energizing, calming, protective
  int vibrationNumber;       // Numerology (1-9)

  // Healing Properties
  List<String> emotionalHealing;
  List<String> physicalHealing;
  List<String> spiritualProperties;

  // Care Instructions
  List<String> cleansingMethods;
  List<String> chargingMethods;
  List<String> cautions;     // e.g., "Do not place in water"

  // Media
  String imageUrl;           // Primary image
  List<String> imageGallery; // Multiple angles

  // Additional
  String description;
  List<String> bestCombinations;
  List<String> keywords;
}
```

### 1.3 Crystal Data Checklist (50 Essential Crystals)

**Quartz Family:**
- [ ] Clear Quartz - Master Healer
- [ ] Rose Quartz - Love Stone
- [ ] Smoky Quartz - Grounding
- [ ] Amethyst - Spiritual Wisdom
- [ ] Citrine - Abundance
- [ ] Ametrine - Balance
- [ ] Rutilated Quartz - Amplification
- [ ] Phantom Quartz - Inner Growth

**Protection Stones:**
- [ ] Black Tourmaline - EMF Protection
- [ ] Obsidian - Shadow Work
- [ ] Black Onyx - Strength
- [ ] Shungite - Purification
- [ ] Jet - Grief Protection
- [ ] Hematite - Grounding Shield

**Heart Chakra:**
- [ ] Green Aventurine - Luck
- [ ] Malachite - Transformation
- [ ] Rhodonite - Emotional Healing
- [ ] Rhodochrosite - Self-Love
- [ ] Prehnite - Unconditional Love
- [ ] Chrysoprase - Joy

**Third Eye/Crown:**
- [ ] Lapis Lazuli - Truth
- [ ] Sodalite - Logic
- [ ] Labradorite - Magic
- [ ] Moonstone - Intuition
- [ ] Selenite - Clarity
- [ ] Fluorite - Mental Focus
- [ ] Lepidolite - Anxiety Relief
- [ ] Charoite - Spiritual Transformation

**Solar Plexus/Sacral:**
- [ ] Tiger's Eye - Confidence
- [ ] Carnelian - Creativity
- [ ] Sunstone - Joy
- [ ] Orange Calcite - Energy
- [ ] Yellow Jasper - Protection
- [ ] Pyrite - Manifestation

**Throat Chakra:**
- [ ] Aquamarine - Communication
- [ ] Blue Lace Agate - Calm Expression
- [ ] Turquoise - Protection & Wisdom
- [ ] Amazonite - Truth Speaking
- [ ] Chrysocolla - Goddess Stone

**Root Chakra:**
- [ ] Red Jasper - Stability
- [ ] Garnet - Passion
- [ ] Bloodstone - Courage
- [ ] Ruby - Vitality

**Rare/Specialty:**
- [ ] Moldavite - Transformation
- [ ] Larimar - Divine Feminine
- [ ] Sugilite - Spiritual Love
- [ ] Kunzite - Heart Opening
- [ ] Tanzanite - Psychic Abilities

### 1.4 Image Requirements

- [ ] **1.4.1** Source royalty-free crystal images (Unsplash, Pexels, or purchase stock)
- [ ] **1.4.2** Upload to Firebase Storage at `/crystals/{crystal_id}/`
- [ ] **1.4.3** Generate thumbnails (150x150, 400x400, 800x800)
- [ ] **1.4.4** Update `crystal_library` Firestore collection with image URLs
- [ ] **1.4.5** Implement image caching in `image_cache_service.dart`

### 1.5 Update Seed Script

**File:** `/scripts/seed_database.js`

- [ ] **1.5.1** Expand from 5 crystals to 50+ crystals
- [ ] **1.5.2** Add all new metadata fields to each entry
- [ ] **1.5.3** Include zodiac/birth sign associations
- [ ] **1.5.4** Add vibration numbers and planetary rulers
- [ ] **1.5.5** Run seed script to populate Firestore

### 1.6 Update AI Guru Context

**File:** `/functions/index.js` (consultCrystalGuru function)

- [ ] **1.6.1** Update system prompt to reference new metadata fields
- [ ] **1.6.2** Include zodiac compatibility in recommendations
- [ ] **1.6.3** Reference chakra alignments for healing suggestions
- [ ] **1.6.4** Use vibration numbers for crystal pairings

---

## 2. AI Model Migration

### Priority: HIGH | Estimated Tasks: 12

Migrate all Gemini AI calls from current models to `gemini-2.5-flash-lite`.

### 2.1 Functions to Update

**File:** `/functions/index.js`

| Function | Current Model | Line | Status |
|----------|---------------|------|--------|
| `identifyCrystal` | `gemini-2.0-flash` | 445 | [ ] Update |
| `getCrystalGuidance` | `gemini-1.5-flash` | 747 | [ ] Update |
| `analyzeDream` | `gemini-1.5-flash` | 1089 | [ ] Update |
| `getPersonalizedCrystalRecommendation` | `gemini-1.5-flash` | 1724 | [ ] Update |
| `analyzeCrystalCollection` | `gemini-1.5-flash` | 1872 | [ ] Update |
| `getPersonalizedDailyRitual` | `gemini-1.5-flash` | 1967 | [ ] Update |
| `getCrystalCompatibility` | `gemini-1.5-flash` | 2043 | [ ] Update |
| `consultCrystalGuru` | `gemini-2.0-flash-exp` | 2242 | [ ] Update |

### 2.2 Migration Steps

- [ ] **2.2.1** Verify `gemini-2.5-flash-lite` is available in @google/generative-ai SDK
- [ ] **2.2.2** Update package.json if newer SDK version required
- [ ] **2.2.3** Create centralized model configuration constant
- [ ] **2.2.4** Update all 8 functions with new model name
- [ ] **2.2.5** Test each function after migration
- [ ] **2.2.6** Deploy updated functions to Firebase

### 2.3 Recommended Code Change

**Before:**
```javascript
const model = genAI.getGenerativeModel({ model: 'gemini-1.5-flash' });
```

**After (with centralized config):**
```javascript
// At top of index.js
const GEMINI_MODEL = 'gemini-2.5-flash-lite';

// In each function
const model = genAI.getGenerativeModel({ model: GEMINI_MODEL });
```

### 2.4 Cost Optimization Settings

- [ ] **2.4.1** Reduce `maxOutputTokens` where appropriate (1024 → 512 for simple responses)
- [ ] **2.4.2** Lower `temperature` for more consistent responses (0.7 → 0.5)
- [ ] **2.4.3** Implement response caching for common queries

---

## 3. Marketplace Functionality

### Priority: HIGH | Estimated Tasks: 18

The marketplace is ~50% complete. Critical missing features need implementation.

### 3.1 Listing Deletion (CRITICAL)

**File:** `/lib/screens/marketplace_screen.dart`

- [ ] **3.1.1** Add delete icon/button to listing cards in "My Listings" tab
- [ ] **3.1.2** Create `_showDeleteConfirmationDialog()` method
- [ ] **3.1.3** Implement `_deleteListing(String listingId)` method
- [ ] **3.1.4** Call Firestore delete (rules already permit seller deletion)
- [ ] **3.1.5** Show success/error snackbar after deletion
- [ ] **3.1.6** Refresh listings grid after deletion

### 3.2 Listing Edit Functionality

- [ ] **3.2.1** Add edit icon/button to listing cards
- [ ] **3.2.2** Create `_showEditListingDialog(MarketplaceListing listing)` method
- [ ] **3.2.3** Pre-populate form with existing listing data
- [ ] **3.2.4** Implement Firestore update call
- [ ] **3.2.5** Refresh listings after edit

### 3.3 Listing Details Screen

- [ ] **3.3.1** Create new file `/lib/screens/listing_details_screen.dart`
- [ ] **3.3.2** Add tap handler to listing cards (GestureDetector/InkWell)
- [ ] **3.3.3** Display full listing information
- [ ] **3.3.4** Show seller contact information
- [ ] **3.3.5** Add "Contact Seller" button
- [ ] **3.3.6** Navigate to details on card tap

### 3.4 Remove Coming Soon Placeholder

**File:** `/lib/screens/marketplace_screen.dart:806`

- [ ] **3.4.1** Remove `ComingSoonCard.crystalSales()` from Sell tab
- [ ] **3.4.2** Replace with actual functionality or remove section entirely

### 3.5 Cloud Function Additions (Optional)

**File:** `/functions/index.js`

- [ ] **3.5.1** Add `deleteListing` Cloud Function with validation
- [ ] **3.5.2** Add `updateListing` Cloud Function with field restrictions
- [ ] **3.5.3** Add seller notification on listing actions

---

## 4. Collections & Journal Fixes

### Priority: MEDIUM | Estimated Tasks: 15

### 4.1 Missing Firestore Security Rules

**File:** `/firestore.rules`

- [ ] **4.1.1** Add rule for `collectionLogs` subcollection:
```
match /users/{userId}/collectionLogs/{logId} {
  allow read, write: if request.auth != null && request.auth.uid == userId;
}
```

### 4.2 Collection Analysis UI (Missing Feature)

The `analyzeCrystalCollection` Cloud Function exists but has no UI.

- [ ] **4.2.1** Create "Analyze Collection" button in collection_screen.dart
- [ ] **4.2.2** Call `FirebaseFunctionsService.analyzeCrystalCollection()`
- [ ] **4.2.3** Display analysis results in modal or new screen
- [ ] **4.2.4** Show element/chakra/energy balance insights
- [ ] **4.2.5** Display AI recommendations for collection gaps

### 4.3 Backend Sync Implementation

**File:** `/lib/services/collection_service.dart:342-349`

- [ ] **4.3.1** Implement `_syncWithBackend()` method or remove TODO
- [ ] **4.3.2** Implement `_syncEntryToBackend()` method or remove TODO
- [ ] **4.3.3** Add retry logic for failed syncs

### 4.4 Journal Improvements

**File:** `/lib/screens/dream_journal_screen.dart`

- [ ] **4.4.1** Add crystal usage logging from collection
- [ ] **4.4.2** Show crystal recommendations in journal entries
- [ ] **4.4.3** Link journal entries to collection crystals

---

## 5. Home Screen UI Redesign

### Priority: HIGH | Estimated Tasks: 20

Major layout changes to improve user experience.

### 5.1 Crystal of the Day - Make Smaller Horizontal Band

**File:** `/lib/screens/home_screen.dart` (lines 249-343)

**Current:** Large vertical card (~450-500px height)
**Target:** Compact horizontal band (~120-150px height)

- [ ] **5.1.1** Change layout from Column to Row
- [ ] **5.1.2** Reduce icon size from 150x150 to 60x60
- [ ] **5.1.3** Reduce title font from 28 to 18
- [ ] **5.1.4** Move properties to expandable section
- [ ] **5.1.5** Add "See More" tap to expand details
- [ ] **5.1.6** Implement horizontal card design:

```dart
// Target Layout:
Row(
  children: [
    // Small crystal icon (60x60)
    CircleAvatar(radius: 30, child: Icon(Icons.diamond, size: 30)),
    SizedBox(width: 16),
    // Crystal info
    Expanded(
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Text('Crystal of the Day', style: TextStyle(fontSize: 12)),
          Text(crystalName, style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
          Text(shortDescription, maxLines: 1, overflow: TextOverflow.ellipsis),
        ],
      ),
    ),
    // Expand button
    IconButton(icon: Icon(Icons.chevron_right), onPressed: _showDetails),
  ],
)
```

### 5.2 Crystal ID & Guru - Make Prominent Cards

**Current:** Crystal ID is buried in 2x3 grid, Guru only in FAB
**Target:** Featured cards below Crystal of the Day

- [ ] **5.2.1** Create new "Quick Actions" section after Crystal of the Day
- [ ] **5.2.2** Create large Crystal ID card (full width or half width)
- [ ] **5.2.3** Create large Guru Consultation card (full width or half width)
- [ ] **5.2.4** Add icon + title + description to each card
- [ ] **5.2.5** Keep Guru FAB as secondary access point
- [ ] **5.2.6** Implement card design:

```dart
// Quick Actions Section
Container(
  padding: EdgeInsets.all(16),
  child: Column(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: [
      Text('Quick Actions', style: Theme.of(context).textTheme.titleLarge),
      SizedBox(height: 12),
      Row(
        children: [
          // Crystal ID Card
          Expanded(
            child: _buildQuickActionCard(
              icon: Icons.camera_alt,
              title: 'Identify Crystal',
              subtitle: 'Scan any crystal',
              color: AppTheme.mysticPink,
              onTap: () => _navigateTo(CrystalIdentificationScreen()),
            ),
          ),
          SizedBox(width: 12),
          // Guru Card
          Expanded(
            child: _buildQuickActionCard(
              icon: Icons.auto_awesome,
              title: 'Crystal Guru',
              subtitle: 'Get AI guidance',
              color: AppTheme.cosmicPurple,
              onTap: () => _showGuruOverlay(),
            ),
          ),
        ],
      ),
    ],
  ),
)
```

### 5.3 Remaining Feature Grid

- [ ] **5.3.1** Move remaining features below Quick Actions
- [ ] **5.3.2** Reduce grid from 6 items to remaining items
- [ ] **5.3.3** Keep consistent card sizing (1:1 aspect ratio)
- [ ] **5.3.4** Maintain existing navigation

### 5.4 New Home Screen Layout Order

```
1. AppBar (Profile button)
2. Crystal of the Day (horizontal band - 120px)
3. Quick Actions (Crystal ID + Guru cards - 150px)
4. Features Grid (remaining features - flexible)
5. Guru FAB (floating, bottom right)
```

### 5.5 Widget Files to Create/Modify

- [ ] **5.5.1** Create `/lib/widgets/compact_crystal_of_day.dart`
- [ ] **5.5.2** Create `/lib/widgets/quick_action_card.dart`
- [ ] **5.5.3** Modify `/lib/screens/home_screen.dart` layout
- [ ] **5.5.4** Keep `/lib/widgets/guru_fab_button.dart` as secondary access

---

## 6. Settings & Configuration Fixes

### Priority: MEDIUM | Estimated Tasks: 18

### 6.1 Disabled Toggle Fixes

**File:** `/lib/screens/settings_screen.dart`

| Feature | Line | Action |
|---------|------|--------|
| Push Notifications | 460-501 | [ ] Implement or hide |
| Dark Mode | 582-623 | [ ] Remove (only dark theme exists) |
| Language Settings | 625-649 | [ ] Implement i18n or hide |
| Meditation Reminders | 709-728 | [ ] Implement or hide |
| Crystal Care Reminders | 754-773 | [ ] Implement or hide |

- [ ] **6.1.1** Either implement push notifications with Firebase Cloud Messaging
- [ ] **6.1.2** OR hide the notification toggle with visibility flag
- [ ] **6.1.3** Remove dark mode toggle (app is dark-only)
- [ ] **6.1.4** Hide language settings until i18n is implemented
- [ ] **6.1.5** Implement local notifications for reminders OR hide toggles

### 6.2 Remove Coming Soon Cards

**Files to update:**
- [ ] **6.2.1** `/lib/screens/moon_rituals_screen.dart:164` - Remove or implement Moon Expert
- [ ] **6.2.2** `/lib/screens/sound_bath_screen.dart:515` - Remove or implement Sound Expert
- [ ] **6.2.3** `/lib/screens/marketplace_screen.dart:806` - Remove Crystal Sales Expert

### 6.3 Environment Configuration

**File:** `/lib/services/environment_config.dart`

- [ ] **6.3.1** Remove hardcoded localhost URLs (lines 129, 133)
- [ ] **6.3.2** Ensure production builds use correct endpoints
- [ ] **6.3.3** Add environment variable validation

**File:** `/lib/config/backend_config.dart`

- [ ] **6.3.4** Remove hardcoded `http://localhost:8081` (line 31)
- [ ] **6.3.5** Add proper fallback for missing configuration

---

## 7. Code Quality & Technical Debt

### Priority: LOW-MEDIUM | Estimated Tasks: 25

### 7.1 Remove Debug Print Statements

**Files with print() statements to remove:**

- [ ] **7.1.1** `/lib/services/firebase_ads_service.dart:67`
- [ ] **7.1.2** `/lib/services/production_ads_service.dart:61`
- [ ] **7.1.3** `/lib/services/guru_service.dart:76,84`
- [ ] **7.1.4** Search for all `print(` statements and replace with proper logging

### 7.2 Remove Backup/Duplicate Files

- [ ] **7.2.1** Delete `/lib/screens/home_screen_backup.dart`
- [ ] **7.2.2** Consolidate crystal models (crystal.dart, crystal_model.dart, crystal_v2.dart)
- [ ] **7.2.3** Review firebase_service_new.dart - merge or delete

### 7.3 Error Handling Improvements

- [ ] **7.3.1** Replace generic `Exception` throws with custom exception types
- [ ] **7.3.2** Fix silent error handling (services returning null on error)
- [ ] **7.3.3** Add user-friendly error messages throughout

### 7.4 Unused Code Cleanup

- [ ] **7.4.1** Remove unused `ComingSoonCard` factory constructors
- [ ] **7.4.2** Remove mock payment classes from production code
- [ ] **7.4.3** Clean up unused imports

### 7.5 Missing Route Definitions

**File:** `/lib/main.dart`

- [ ] **7.5.1** Add `/marketplace` route
- [ ] **7.5.2** Add `/collection` route
- [ ] **7.5.3** Add `/crystal-id` route
- [ ] **7.5.4** Add `/journal` route
- [ ] **7.5.5** Add `/subscription-success` route

---

## 8. Authentication & Security

### Priority: HIGH | Estimated Tasks: 8

### 8.1 OAuth Implementation

**File:** `/lib/services/firebase_service.dart`

- [ ] **8.1.1** Implement `signInWithGoogle()` method (line 380)
- [ ] **8.1.2** Implement `signInWithApple()` method (line 387)
- [ ] **8.1.3** OR clearly document that OAuth is manual-only via Firebase Console

### 8.2 Security Rule Updates

**File:** `/firestore.rules`

- [ ] **8.2.1** Add missing `collectionLogs` rule
- [ ] **8.2.2** Review all rules for completeness
- [ ] **8.2.3** Add rate limiting considerations

---

## Implementation Priority Order

### Phase 1: Critical Fixes (Week 1)
1. [ ] AI Model Migration to Gemini 2.5 Flash Lite
2. [ ] Marketplace Deletion Functionality
3. [ ] Home Screen UI Redesign

### Phase 2: Data Enhancement (Week 2)
4. [ ] Crystal Database Enhancement (50 crystals)
5. [ ] Crystal Images Upload
6. [ ] Update Seed Script

### Phase 3: Features & Polish (Week 3)
7. [ ] Collections Analysis UI
8. [ ] Settings Cleanup
9. [ ] Coming Soon Card Removal

### Phase 4: Technical Debt (Week 4)
10. [ ] Code Quality Fixes
11. [ ] Authentication Completion
12. [ ] Route Definitions

---

## Testing Checklist

After each phase, verify:

- [ ] All AI functions respond correctly with new model
- [ ] Marketplace listings can be created, edited, and deleted
- [ ] Home screen displays correctly on mobile and web
- [ ] Crystal of the Day shows in compact horizontal format
- [ ] Crystal ID and Guru cards are prominent
- [ ] Collection analysis displays insights
- [ ] No console errors or warnings
- [ ] Build completes without errors

---

## Deployment Commands

```bash
# Deploy all changes
cd /home/user/crystal-grimoire-development

# Deploy functions only (after AI model changes)
firebase deploy --only functions --project crystal-grimoire-2025

# Deploy hosting (after Flutter changes)
flutter build web --release
firebase deploy --only hosting --project crystal-grimoire-2025

# Deploy Firestore rules
firebase deploy --only firestore:rules --project crystal-grimoire-2025

# Full deployment
firebase deploy --project crystal-grimoire-2025
```

---

## Progress Tracking

| Category | Total | Completed | Percentage |
|----------|-------|-----------|------------|
| Crystal Database | 25 | 0 | 0% |
| AI Migration | 12 | 0 | 0% |
| Marketplace | 18 | 0 | 0% |
| Collections | 15 | 0 | 0% |
| Home Screen UI | 20 | 0 | 0% |
| Settings | 18 | 0 | 0% |
| Code Quality | 25 | 0 | 0% |
| Authentication | 8 | 0 | 0% |
| **TOTAL** | **141** | **0** | **0%** |

---

**Document Version:** 1.0
**Created:** December 5, 2025
**Last Updated:** December 5, 2025

---

*This document should be updated as tasks are completed. Check off items as they are finished and update the progress tracking table.*
