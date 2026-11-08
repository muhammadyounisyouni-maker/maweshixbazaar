# Maweshix Bazar - Stage 1 Prototype

Front-end design prototype (single file, no build step).

## Run (Windows)
Double-click `index.html`, or serve it:
    python -m http.server 8000
then open http://localhost:8000

## Included
Urdu/English with RTL/LTR, home, browse + filters + voice search,
details dialog (tel / wa.me), 6-step sell wizard, help & safety.

## Not included yet
FastAPI backend, PostgreSQL, OTP, image storage, real admin auth,
favorites, reports. Listings are sample data; new ads vanish on refresh.

## Trust flow (demo)
New ads start as "pending" and appear in Browse only after admin approval.
Admin panel: open Help page > "Admin (demo)", PIN 1234 (demo only; real
admin auth must be enforced on the server). Admin can approve/reject ads,
give or remove the Verified badge, handle reports, and see an action log.

## Contact Admin (demo)
Bottom-nav 'Admin' tab: call/WhatsApp the admin (sample number) or send an issue form. Messages appear in the Admin panel with a Resolved button. No backend yet.

## Buying flow (demo)
Animal details -> Add to cart -> Cart (3 steps: cart, your details, admin confirmation)
-> purchase request goes to the Admin panel (tab "Purchase requests"):
requested -> contacted -> completed (ad becomes Sold) or cancelled (ad active again).
No online payment. Admin panel is opened from the footer (demo PIN 1234).

## Stage 2: repairs + vet doctor verification (demo)
Menu (☰ in header): Favorites, My Listings, Find a Vet Doctor, Doctor Registration/Dashboard,
Profile & Settings, Help, Contact, Admin, Logout.
Data is saved in this browser's localStorage only (NOT a server). Roles/PIN are demo only.
Doctor flow: register -> pending -> admin (Admin > Veterinary Doctor Verification) approves/rejects/
requests documents/suspends -> only then listed as Verified. A doctor cannot approve themselves.
PDF uploads store only the file name in this demo; real document storage needs the backend.

## Stage 3: e-commerce layout + themes
Header: search (with voice), cart/favorites badges, theme toggle (Light or Dark; first visit follows the device, then saved in this browser), language, menu.
Shop: category chips, filters sidebar (city, price min/max), sort, result count, Load more; cards have Add to Cart + Buy Now.

## Stage 4: e-commerce landing page
Home: swipeable banners (buy / sell / vet doctors), trust tiles, shop by category, shop by budget,
new arrivals, verified sellers, sell banner, how it works.

## Stage 5: payments (manual, demo)
Cart offers JazzCash, Easypaisa and Bank Transfer. The ADMIN enters the real account details
(Admin > Payments); nothing is hard-coded. Buyer pays outside the app and submits the TID;
admin confirms "payment received"; only then can an order be completed (animal becomes Sold).
Automatic JazzCash/Easypaisa checkout needs merchant accounts and the backend.

## Stage 6: branding
Name: Maweshix Bazar (مویشیکس بازار). Header logo and hero banner are embedded in index.html
(originals in assets/). The banner name was edited from the uploaded picture; the cow, buffalo,
sheep, goat and M-bull logo are from the uploaded artwork.

## Stage 7: unique landing + smoothness
Emerald-and-gold heritage landing (patterned full-width hero, floating banner, count-up stats, category/city ticker,
category tiles with live counts, feature cards). Smooth scroll, page transitions, reveal-on-scroll, dialog animation,
button press feedback. All motion is switched off for visitors who set "reduce motion".

## Stage 8: real animal photos + trust follow-ups
Category tiles, cards, details, cart and the sell wizard now use real animal photos cropped from the supplied artwork
(embedded in index.html as PIC). Sellers' own uploaded photos still take priority on their listings.
Also: "admin present" purchase option with admin-scheduled meeting, complaint/refund flow after completed orders,
admin button to remove sample listings (before going live, delete the sample L array entries in index.html too).

## Stage 9: smart search + voice fix
Header search: suggestions (categories with photos, cities, matching ads with price), recent searches, highlight, clear button,
keyboard (arrows/Enter/Esc), live filtering on the Browse page. Voice: live words in the box, recording state, Urdu locale
fallback (ur-PK -> ur-IN -> en-PK), and specific messages for denied permission / no speech / no mic / network.
Voice needs a browser with SpeechRecognition (Chrome/Edge/Android Chrome) and microphone permission; embedded previews
(iframes) often block the microphone, so open the page in its own tab.

## Stage 10: full-background hero
The landing hero now uses the artwork (animals + M-bull logo) as a full-width background with a dark shadow fade;
the name is live text over it. Original files: assets/maweshix-bazar-banner.png, assets/hero-background.jpg.

## Stage 11: smoother landing + image
Hero image: sharper (2200px), fades in on load, slow zoom, gentle parallax on scroll; hero text rises in step by step.
Animal photos are stored once as CSS classes (.pic-cow etc.) instead of repeated in the HTML, so pages render lighter on cheap phones.
Light and dark hero looks are both kept (default theme is light).

## Stage 12: 3D animals
Category tiles, the sell wizard and cards without a seller photo now show cut-out animals popping out of a gold-ringed disc
(assets/cutouts/*.png), with a 3D tilt + glare on hover (desktop), a gentle float, and depth shadows. The cut-outs were made
automatically from the supplied artwork, so edges are not studio quality. These are 3D-style effects on photos, not real 3D models:
a true 3D model viewer needs model files (GLB) of each animal.
Bug fixed: the animal photos had disappeared after the previous update (a CSS shorthand wiped them); a test now guards this.

## Stage 13: accounts, onboarding, plans
- Header button: "سائن اپ / لاگ ان" (shows the user's first name when logged in).
- Sign up: name, phone, who you are (buyer / seller / veterinary doctor), city. Login: phone number (demo, no OTP yet).
  Sellers are sent to Sell, doctors to Doctor Registration, buyers to Browse.
- First visit: "خوش آمدید! آپ کون ہیں؟" asks who the visitor is, then opens sign up with that role.
- Publishing an ad requires login. Ad limit follows the plan: Basic 3 active ads (free), Silver 10 (PKR 1,500/month),
  Gold unlimited (PKR 3,000/month). Prices are proposals; plan requests are approved by the admin
  (Admin > "پیکیج درخواستیں"). No automatic payment yet.
- Category tiles: gold ring removed; animals sit directly on the card.
Demo limits: accounts and roles live in this browser only; login is by phone number without a password or OTP.
A real backend must add OTP login, server-side role checks and real payments before going live.

## Stage 14: notifications + email login
- First-time visitor: role-pick onboarding (as before), which leads into sign up.
- Returning visitor who never logged in: gets a one-time-per-session toast reminding them to sign up or log in
  (does not block browsing). Logged-in visitors never see it.
- Admin notifications (Admin panel > "اطلاعات", unread count badge): fires when a new member signs up, a seller
  submits an ad, a buyer sends a purchase request, a doctor submits a registration, or a buyer sends a consultation
  request. Admin can mark one or all as read.
- Sign up now also takes an optional email (unique, validated). Log in accepts either the phone number or the email
  in one field (detected automatically). Still demo-only: no password or OTP, data lives in this browser.
