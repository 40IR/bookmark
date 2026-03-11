javascript:(function(){
  const url = 'https://40ir.github.io/bookmark/bookmarklet/midnight.js?' + Date.now();
  fetch(url)
    .then(r => { if (!r.ok) throw new Error('HTTP '+r.status); return r.text(); })
    .then(js => {
      let code = js.trim();
      if (code.toLowerCase().startsWith('javascript:')) code = code.slice(11);
      console.log('✅ Midnight loaded — running latest version from GitHub');
      const s = document.createElement('script');
      s.textContent = code;
      (document.head || document.documentElement).appendChild(s);
      // s.remove(); // uncomment if you want to clean up after running
    })
    .catch(err => {
      console.error('❌ Midnight fetch failed:', err);
      alert('❌ Could not load from GitHub\n\n' + err + '\n\nOpen F12 console for details.');
    });
})();
