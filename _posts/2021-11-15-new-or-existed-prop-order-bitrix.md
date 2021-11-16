---
layout: post
title: Работа со свойством заказа в d7 Bitrix. 1С-Битрикс
---

Возникла потребность при разделении заказа в 1С на подзаказы, выражать это в свойстве "Номер подзаказа".
Завязываемся на событие "OnSaleOrderSaved".
```
$eventManager = \Bitrix\Main\EventManager::getInstance();
$eventManager->addEventHandler(
    'sale',
    'OnSaleOrderSaved',
    'addOrderPropertyUnnumber'
);

function addOrderPropertyUnnumber(\Bitrix\Main\Event $event) {

    /** @var \Bitrix\Sale\Order $order */
    $order = $event->getParameter("ENTITY");
    $id = $order->getId();
    $propertyCode = 'UNNUMBER_NUM';

    /** @var \Bitrix\Sale\PropertyValueCollection $propertyCollection */
    $propertyCollection = $order->getPropertyCollection();

    $property = null;
    if($propertyCollection->getItemByOrderPropertyCode($propertyCode) === null) {
        $property = $propertyCollection->createItem(
            [
                'NAME' => 'Номер подзаказа',
                'CODE' => $propertyCode,
                'TYPE' => 'STRING',
            ]
        );
    } else {
        $property = $propertyCollection->getItemByOrderPropertyCode($propertyCode);
    }
    if($property && !$property->getValue()) {
        $property->setField('VALUE', $id.'_1');
        $order->save();
    }
}
```
