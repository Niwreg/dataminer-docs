---
uid: config_resource_automation
---

# Additional configuration for Resource Automation

## Default wizard included in the SRM framework

When you install the SRM framework, an Automation script is included that can be used as the default wizard to apply a profile to a resource.

### Required input parameters

The wizard is an interactive Automation script called *SRM_ApplyProfileToResource*. As of SRM version 1.2.27, the input parameters accept the following fields in JSON format:

- *ResourceId*: The GUID of the resource that will be used by the wizard.
- *BookingManagerName*: Optional. The name of a Booking Manager element. This is used to generate log files in the directory specified in that element.
- *ReservationId*: Optional. The GUID of a booking, in case the profile instance needs to be applied in the context of a booking. This is only valid for bookings that are currently active.

For example: `{"ResourceId":" 25405e6e-3f96-4801-bc76-2dc1dae18358"}`

> [!NOTE]
> For an up-to-date definition of the input argument, import *SLSRMLibrary.dll* and check the class *Skyline.DataMiner.Library.Solutions.SRM.Model.ApplyProfileToResource.InputData*.

### Running the wizard

When a user runs the wizard, they will need to select a profile instance, and they can optionally also select a target service state.

![SRM_ApplyProfileToResource wizard](~/user-guide/images/srm_applyprofiletoresource.png)

After that, they only need to click *Apply* to apply the selected profile instance to the resource.

## Creating a custom front end for the wizard

The wizard can be launched from Visual Overview or from a low-code app.

A typical use case is to make use of the Resource Manager component in Visual Overview, showing resource bands on the Y-axis:

1. Embed a Resource Manager component in your Visio drawing, and use the *YAxisResources* variable to define the resources that will be listed on the Y-axis. See [Embedding a Resource Manager component](xref:Embedding_a_Resource_Manager_component).

   When a user selects a resource band on the timeline, the *SelectedResource* variable will be populated with the GUID of the resource.

1. Add a shape to the Visio drawing that executes the *SRM_ApplyProfileToResource* script, using the expected JSON as the input argument. See [Linking a shape to an Automation script](xref:Linking_a_shape_to_an_Automation_script).

   Use a variable placeholder in the JSON to reference the selected resource. For example:

   `script:SRM_ApplyProfileToResource||Input Data={"ResourceId":"[cardvar:SelectedResource]"}|||NoConfirmation,CloseWhenFinished`
