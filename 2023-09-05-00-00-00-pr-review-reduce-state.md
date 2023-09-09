# Today I Reviewed: Use single state instead of three

Received a pull request, like the following

```typescript
const SomeComponent = () => {
  const [isStatusPageModalOpen, setIsStatusPageModalOpen] = useState(false);
  const [isEditProbeModalOpen, setIsEditProbeModalOpen] = useState(false);
  const [isDeleteProbeModalOpen, setIsDeleteProbeModalOpen] = useState(false);

  return (
    <div>
      {isStatusPageModalOpen ? <StatusPageModal /> : null}
      {isEditProbeModalOpen ? <EditProbeModal /> : null}
      {isDeleteProbeModalOpen ? <DeleteProbeModal /> : null}
    </div>
  )
}
```

The problem with the code is that there can only be one modal appear at the same time. So using three states for this is a waste and could cause unintentional bug where two or three modals appear at the same time. 

Instead, it's better to use a single state like the following

```typescript
type ModalOpenType = 'edit' | 'delete' | 'status'
const [openedModal, setOpenedModal] = useState<ModalOpenType | null>(null);

return  (
    <div>
      {openedModal === 'status' ? <StatusPageModal /> : null}
      {openedModal === 'edit' ? <EditProbeModal /> : null}
      {openedModal === 'delete' ? <DeleteProbeModal /> : null}
    </div>
  )
```
