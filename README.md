<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ABODE3'S Hostel Agency</title>
<style>
  body { font-family: Arial, sans-serif; background: #f5f5f5; margin: 0; padding: 0; }
  header { background: #0f4c63; color: white; padding: 15px; text-align: center; }
  h1 { margin: 0; }
  .container { max-width: 900px; margin: auto; padding: 15px; background: white; }
  .amenities { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 10px; }
  .amenity { border: 1px solid #ddd; border-radius: 5px; overflow: hidden; background: #fafafa; text-align: center; }
  .amenity img { width: 100%; height: 150px; object-fit: cover; }
  form { margin-top: 20px; }
  input, select, button { width: 100%; padding: 10px; margin-top: 10px; border-radius: 5px; border: 1px solid #ccc; }
  button { background: #0f4c63; color: white; border: none; cursor: pointer; }
  button:hover { background: #0c3a4d; }
  .preview { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 10px; }
  .preview div { position: relative; }
  .preview img, .preview video { width: 120px; height: 100px; object-fit: cover; border-radius: 5px; }
  .remove { position: absolute; top: 2px; right: 2px; background: rgba(255,0,0,0.8); color: white; border: none; border-radius: 3px; padding: 2px 5px; cursor: pointer; font-size: 12px; }
</style>
</head>
<body>
<header>
  <h1>ABODE3'S Hostel Agency</h1>
  <p>Comfortable & Affordable Accommodation</p>
</header>
<div class="container">
  <h2>Amenities</h2>
  <div class="amenities">
    <div class="amenity">
      <img src="https://images.unsplash.com/photo-1505691723518-36a8b3f3f2fd?w=800" alt="Bed and Mattress">
      <p><strong>Bed and Mattress</strong></p>
    </div>
    <div class="amenity">
      <img src="https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=800" alt="Wardrobe">
      <p><strong>Wardrobe</strong></p>
    </div>
    <div class="amenity">
      <img src="https://images.unsplash.com/photo-1504674900247-0877df9cc836?w=800" alt="Kitchen">
      <p><strong>Kitchen</strong></p>
    </div>
    <div class="amenity">
      <img src="https://images.unsplash.com/photo-1560448204-e02f11c3d0e2?w=800" alt="Washroom">
      <p><strong>Washroom</strong></p>
    </div>
  </div>

  <h2>Upload Hostel Photos & Videos</h2>
  <input type="file" id="mediaInput" accept="image/*,video/*" multiple>
  <div class="preview" id="preview"></div>

  <h2>Book an Accommodation</h2>
  <form id="bookingForm">
    <input type="text" id="name" placeholder="Full Name" required>
    <input type="email" id="email" placeholder="Email">
    <input type="tel" id="phone" placeholder="Phone Number">
    <select id="contactNumber">
      <option value="0597053192">Main — 0597053192</option>
      <option value="0594708232">Alt 1 — 0594708232</option>
      <option value="0594438054">Alt 2 — 0594438054</option>
    </select>
    <button type="submit">Send Booking via WhatsApp</button>
  </form>
</div>
<script>
  const countryCode = '+233'; // Ghana

  document.getElementById('mediaInput').addEventListener('change', function(e) {
    const preview = document.getElementById('preview');
    preview.innerHTML = '';
    Array.from(e.target.files).forEach(file => {
      const url = URL.createObjectURL(file);
      const wrapper = document.createElement('div');
      let mediaEl;
      if (file.type.startsWith('video')) {
        mediaEl = document.createElement('video');
        mediaEl.src = url;
        mediaEl.controls = true;
      } else {
        mediaEl = document.createElement('img');
        mediaEl.src = url;
      }
      const removeBtn = document.createElement('button');
      removeBtn.textContent = 'X';
      removeBtn.className = 'remove';
      removeBtn.onclick = () => wrapper.remove();
      wrapper.appendChild(mediaEl);
      wrapper.appendChild(removeBtn);
      preview.appendChild(wrapper);
    });
  });

  document.getElementById('bookingForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const name = document.getElementById('name').value;
    const email = document.getElementById('email').value;
    const phone = document.getElementById('phone').value;
    const selectedNumber = document.getElementById('contactNumber').value;
    let digits = selectedNumber.replace(/\D/g, '');
    if (digits.startsWith('0')) digits = countryCode.replace('+','') + digits.slice(1);
    const message = `Hello ABODE3'S HOSTEL AGENCY,%0AI would like to book an accommodation.%0AName: ${name}%0AEmail: ${email}%0APhone: ${phone}`;
    window.open(`https://wa.me/${digits}?text=${message}`, '_blank');
  });
</script>
</body>
</html>
