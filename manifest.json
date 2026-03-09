// Delibreads · Service Worker
const CACHE = "delibreads-v1";

self.addEventListener("install", e => {
  self.skipWaiting();
});

self.addEventListener("activate", e => {
  e.waitUntil(clients.claim());
});

// Mantener la app disponible offline (cache básico)
self.addEventListener("fetch", e => {
  e.respondWith(fetch(e.request).catch(() => caches.match(e.request)));
});

// Recibir notificaciones push (para uso futuro con servidor)
self.addEventListener("push", e => {
  const data = e.data?.json() || {};
  self.registration.showNotification(data.title || "Delibreads", {
    body: data.body || "",
    icon: "/icon.png",
    badge: "/icon.png",
    tag: "delibreads-push",
    vibrate: [200, 100, 200],
  });
});

// Al pulsar la notificación, abrir la app
self.addEventListener("notificationclick", e => {
  e.notification.close();
  e.waitUntil(
    clients.matchAll({ type: "window" }).then(list => {
      if (list.length > 0) return list[0].focus();
      return clients.openWindow("/");
    })
  );
});
