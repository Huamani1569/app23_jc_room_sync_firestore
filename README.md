# App23 · Pedidos offline con Room y sincronización con Cloud Firestore

**Desarrollo de Aplicaciones Móviles · Semana 10 · Universidad Continental**  
Autor: Jean Piero Huamani Rodriguez

Misma app de pedidos offline-first de app22, pero la nube es **Cloud Firestore**: los pendientes se envían en un **WriteBatch** atómico (todos o ninguno) y cada pedido se guarda en `pedidos/{uuid}`, así un reenvío sobrescribe el mismo documento y no se duplica. Las **reglas de seguridad** validan los datos (campos exactos, cantidad entera > 0, `recibidoEn == request.time`).

## Estructura
```
model/ Pedido, PedidoMapper (documento con Timestamp y serverTimestamp), PedidoRepository, MonitorConexion
       local/  PedidoEntity, PedidoDao, AppDatabase (Room)
       remote/ PedidoRemoteDataSource (WriteBatch + withTimeoutOrNull)
viewmodel/ PedidoUiState, PedidoViewModel
view/ PantallaPedidos, BannerConexion, PanelSincronizacion, FormularioPedido, PedidoItem
```

## Reglas de Firestore
Ver `firestore.rules`.
