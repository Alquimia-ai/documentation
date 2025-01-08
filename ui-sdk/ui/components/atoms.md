# Atom Components

Core building blocks of the Alquimia UI system. These components are built following shadcn's standards and are fully customizable using Tailwind CSS.

All the components are capable of receiving props and custom classnames.

## Form Components

### Input

Text input component with support for various states and styles.

```tsx
<Input placeholder="Enter your name" />
```

### Textarea

Multi-line text input for longer form content.

```tsx
<Textarea placeholder="Write your message" />
```

### Select

Dropdown selection component with customizable options.

```tsx
<Select {...props}>
  <SelectTrigger aria-label="Food">
    <SelectValue placeholder="Select a fruit..." />
  </SelectTrigger>
  <SelectContent>
    <SelectGroup>
      <SelectLabel>Fruits</SelectLabel>
      <SelectItem value="apple">Apple</SelectItem>
      <SelectItem value="banana">Banana</SelectItem>
      <SelectItem value="grapes">Grapes</SelectItem>
    </SelectGroup>
  </SelectContent>
</Select>
```

### Checkbox

Selectable checkbox component with label support.

```tsx
<Checkbox id="terms" />
<Label htmlFor="terms">Accept terms</Label>
```

### Switch

Toggle switch for boolean settings.

```tsx
<Switch {...props} checked={true} defaultChecked={false} />
```

### Label

Form label component with proper accessibility.

```tsx
<Label htmlFor="email">Email address</Label>
```

### Slider

Range input component for numerical values.

```tsx
<Slider defaultValue={[50]} max={100} step={1} />
```

## Display Components

### Avatar

User avatar display with fallback support.

```tsx
<Avatar>
  <AvatarImage src="user.jpg" />
  <AvatarFallback>JD</AvatarFallback>
</Avatar>
```

### Badge

Status indicator or label component.

```tsx
<Badge variant="success">Completed</Badge>
```

### Card

Container for related content.

```tsx
<Card>
  <CardHeader>
    <CardTitle>Title</CardTitle>
    <CardDescription>Description</CardDescription>
  </CardHeader>
  <CardContent>Content</CardContent>
</Card>
```

### Skeleton

Loading state placeholder.

```tsx
<Skeleton className="h-4 w-[200px]" />
```

### AspectRatio

Maintains consistent width/height ratios.

```tsx
<AspectRatio ratio={16 / 9}>
  <img src="image.jpg" alt="Image" />
</AspectRatio>
```

### Typography

Text components with predefined styles.

```tsx
<Typography typeStyle="display">{value}</Typography>
```

## Interactive Components

### Button

Multi-purpose button component with variants.

```tsx
<Button variant="default" size="sm">Click me</Button>
<Button variant="outline" size="sm">Cancel</Button>
```

### Toggle

Togglable button component.

```tsx
<Toggle variant="default" size="sm">
  Toggle
</Toggle>
```

## Navigation Components

### Tabs

Tabbed interface component.

```tsx
<Tabs layout="centered">
  <TabsList>
    {tabs.map((tab) => (
      <TabsTrigger key={tab.value} value={tab.value}>
        {tab.label}
      </TabsTrigger>
    ))}
  </TabsList>
  {tabs.map((tab) => (
    <TabsContent key={tab.value} value={tab.value}>
      {tab.content}
    </TabsContent>
  ))}
</Tabs>
```

### Breadcrumb

Navigation path indicator.

```tsx
const separator = <span style={{ margin: "0 4px" }}>|</span>

<Breadcrumb aria-label="breadcrumb">
    <BreadcrumbList>
    {items.map((item, index) => (
        <BreadcrumbItem key={index}>
        {item.current ? (
            <BreadcrumbPage>{item.label}</BreadcrumbPage>
        ) : (
            <BreadcrumbLink href={item.href}>{item.label}</BreadcrumbLink>
        )}
        {index < items.length - 1 &&
            (separator ? separator : <BreadcrumbSeparator />)}
        </BreadcrumbItem>
    ))}
    </BreadcrumbList>
</Breadcrumb>
```

## Overlay Components

### Dialog

Modal dialog for important content.

```tsx
<Dialog open={isOpen} onOpenChange={onClose}>
  <DialogTrigger>Open</DialogTrigger>
  <DialogContent aria-describedby={"document-description"}>
    <DialogHeader>
      <DialogTitle>Dialog Title</DialogTitle>
    </DialogHeader>
  </DialogContent>
</Dialog>
```

### Popover

Floating content container.

```tsx
<Popover>
  <PopoverTrigger>Info</PopoverTrigger>
  <PopoverContent>Details here</PopoverContent>
</Popover>
```

### Toast

Notification system component. This component is intented to use with the Toaster component generally placed in the root of the application. this is initializes the context for the toast, and can be used across the app with the useToast hook.

```tsx
const { toast } = useToast();
<html lang="en">
  <body className={nunito.className}>
    {children}
    <Toaster />
    <Button
      variant="outline"
      onClick={() => {
        toast({
          title: "Scheduled: Catch up ",
          description: "Friday, February 10, 2023 at 5:57 PM",
          action: (
            <ToastAction altText="Goto schedule to undo">Undo</ToastAction>
          ),
        });
      }}
    >
      Add to calendar
    </Button>
  </body>
</html>;
```

## Data Display

### Table

Data table with sorting and selection.

```tsx
<Table>
  {caption && <TableCaption>{caption}</TableCaption>}
  <TableHeader>
    <TableRow>
      {headers.map((header, index) => (
        <TableHead key={index}>{header}</TableHead>
      ))}
    </TableRow>
  </TableHeader>
  <TableBody>
    {data.map((row, rowIndex) => (
      <TableRow key={rowIndex}>
        {row.map((cell, cellIndex) => (
          <TableCell key={cellIndex}>{cell}</TableCell>
        ))}
      </TableRow>
    ))}
  </TableBody>
  <TableFooter>
    <TableRow>
      <TableCell colSpan={headers.length}>Footer content</TableCell>
    </TableRow>
  </TableFooter>
</Table>
```

### ScrollArea

Customizable scrollable container.

```tsx
<ScrollArea className="flex-grow mb-4">
  <div>Scrollable content</div>
</ScrollArea>
```

## Feedback Components

### Alert

Contextual feedback messages.

```tsx
<Alert variant="info">
  <AlertTitle>Info</AlertTitle>
  <AlertDescription>Update completed.</AlertDescription>
</Alert>
```

### Loader

Loading state indicator.

```tsx
<Loader size="default" />
```

### RichText

Formatted text content display.

```tsx
<RichText content={markdownContent} />
```

## Utility Components

### Drawer

Side panel component.

```tsx
<Drawer>
  <DrawerTrigger>Open</DrawerTrigger>
  <DrawerContent>
    <DrawerHeader>
      <DrawerTitle>Title</DrawerTitle>
      <DrawerDescription>
        Description
      </DrawerDescription>
    </DrawerHeader>
    Drawer content
  </DrawerContent>
</Drawer>
```
